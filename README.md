# ES_Projekt

## Stage 1 - Requirement Analysis

### 1.1.1 Functional Requirements
**FR1.** The leader robot shall explore the environment autonomously using SLAM.

**FR2.** The follower robot shall maintain a distance of 0.5 ‡ 0.2m behind the leader.

**FR3.** If the follower's distance exceeds 1.5m, the leader shall pause and wait.

**FR4.** If the leader detects a dead end (all forward paths blocked), it shall signal the follower and execute a reversal manoeuvre.

**FR5.** It the follower loses contact with the leader (no status message for > 5s), the follower shall execute a search procedure and the leader shall halt.

**FR6.** Both robots shall recover from every edge case without operator intervention, within the time bounds specified in the timed automata model.

### 1.1.2 Safety Requirements
**SR1**. The system shall never deadlock — at least one robot must always be able to make
progress.
**SR2**. The follover shall not drive closer than 0.2 mn to any obstacle.
**SR3.** The maximum time spent in any waiting state shall be bounded (see Table).

| State | Robot | Max duration |
|---|---|---|
| `WAITING_FOR_FOLLOWER` | Leader | 60s |
| `DEAD_END` | Leader | 15s |
| `WAITING_FOR_LOST_FOLLOWER` | Leader | 120s |
| `APPROACHING` | Follower | 60s |
| `SEARCHING_FOR_LEADER` | Follower | 90s |

### 1.1.3 Safety and liveness properties
**Safety: ** FR2, SR2
 **Liveness: ** FR1, FR3, FR4, FR5, FR6, SR1, SR3

 ### 1.2 Edge Cases
Real cooperative robot systems must be robust. The following edge cases are part of the formal specification and must be handled by your implementation:

**EC1.** Follower too far. The leader starts moving but the follower has not yet reached the correct following distance. The leader must wait while the follower approaches.

**EC2.** Leader hits a dead end. The leader detects that all forward paths are blocked by obstacles. It signals the follower to back up, reverses out, and resumes exploration. The follower temporarily drives forward to keep the path clear.

**EC3.** Follower loses the leader. Signal timeout or excessive distance causes the follower to lose track. The follower searches using the last known position; the leader halts and broadcasts its location until the follower recovers.

**EC4.** Both robots stuck (mutual wait). If both robots are simultaneously waiting for the other, the system must eventually time out and recover - not deadlock indefinitely.
    -> Both robots wait for each other, meaning none of them is looking for the other one. Without the timeout bounds, they would wait forever (for one to find the other one) and the system would be in a deadlock.

**EC5.** The follower doesn't find the leader. After the leader waited for the lost follower for 120 seconds it goes into a safe stop position. 

*!!! Missing:  List any additional edge case you think the specification is missing. Justify your
answer.*

## Stage 2 - State Machine Modelling
-> The goal of this stage is to create precise, readable statechart models for both robots. Statecharts are the bridge between informal requirements and formal timed automata.




