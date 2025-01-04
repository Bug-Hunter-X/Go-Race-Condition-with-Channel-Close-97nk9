# Go Race Condition with Channel Close

This repository demonstrates a subtle race condition in Go that can occur when dealing with channels and goroutines.  The program sends 5 values into a channel and then closes it.  A second goroutine receives from this channel until it's closed. While this seems correct at first, problems may arise under different loads.

## Bug Description
The issue arises when the receiver goroutine continues to receive from the closed channel in the `for...range` loop. It's a subtle condition, but if the receiver is unexpectedly fast or there are further operations on the channel, it could lead to a panic or unexpected behavior if the channel operation is not properly handled.

## Solution
The solution involves careful handling of channel closure and preventing further operations on the closed channel.