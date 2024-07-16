# Survived Robots Health Analysis

This repository contains a Python solution to analyze the survival of robots based on their positions, healths, and movement directions.

## Problem Description

Given three lists:
- `positions`: List of integer positions of robots.
- `healths`: List of integer health values of robots.
- `directions`: String representing movement directions ('R' for right, 'L' for left).

The task is to simulate collisions between robots and determine the healths of robots that survive after all collisions have been resolved.

## Solution

The solution involves the following steps:

1. **Initialization**: Combine positions, healths, and directions into a list of tuples (`nl`) and sort them based on positions.
   
2. **Collision Handling**: Use a stack (`stack`) to accumulate health values of robots moving right ('R'). When encountering a robot moving left ('L'), simulate collisions:
   - If the health of the right-moving robot (`stack[-1]`) is greater, decrement its health.
   - If healths are equal, both robots are destroyed.
   - Otherwise, decrement the health of the left-moving robot and remove the right-moving robot from the stack.

3. **Survival Determination**: After processing all robots:
   - If `left` list is empty, return healths of robots remaining in the `stack`.
   - If `stack` is empty, return healths of robots remaining in the `left` list.
   - Otherwise, combine robots from both lists, sort them by their original indices, and return their healths.

## Example Usage

```python
from typing import List

class Solution:
    def survivedRobotsHealths(self, positions: List[int], healths: List[int], directions: str) -> List[int]:

        def collision(n):
            while stack:
                if stack[-1][1] > n[1]:
                    stack[-1][1] -= 1
                    return
                elif stack[-1][1] == n[1]:
                    stack.pop()
                    return
                else:
                    n[1] -= 1
                    stack.pop()
            left.append(n)
                
        nl = []
        p, h, d = positions, healths, directions
        
        if d == "R" * len(d) or d == "L" * len(d):
            return h
        
        for i in range(len(p)):
            nl.append([p[i], h[i], d[i], i + 1])
        nl.sort()
        stack = []
        left = []
        
        for i in range(len(nl)):
            if nl[i][2] == "R":
                stack.append(nl[i])
            else:
                collision(nl[i])
                
        if left == []:
            stack = sorted(stack, key=lambda x: x[3])
            return [x[1] for x in stack]
        elif stack == []:
            left = sorted(left, key=lambda x: x[3])
            return [x[1] for x in left]
        else:
            if len(left) + len(stack) != len(p):
                result = sorted(left + stack, key=lambda x: x[3])
                return [x[1] for x in result]
            else:
                return h

# Example usage:
if __name__ == "__main__":
    positions = [1, 2, 3, 4]
    healths = [10, 20, 30, 40]
    directions = "RLRR"
    
    sol = Solution()
    result = sol.survivedRobotsHealths(positions, healths, directions)
    
    print("Healths of surviving robots:", result)
