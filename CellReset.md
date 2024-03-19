# Cell Reset Instructions
I'm fairly sure these only work on interior cells but might work on the child interior cell of a worldspace cell. 

> So it make it work, you change iHoursToRespawncell & iHoursToRespawncellCleared to 1 and THEN you type pcb in the console [^1]
> to purge all cells from the buffer. If you now forward time / change the timescale to let one hour pass, all cells will reset!!!

## Instructions

1. In game goto an interrior cell and open the console.
2. Run to force the cell reset.
  - setgs iHoursToRespawncell 1
  - setgs iHoursToRespawncellCleared 1
  - set timescale to 99999
  - pcb
3. Close console and after 10 seconds reopen the console.
4. Run to restore default values.
  - setgs iHoursToRespawncell 168
  - setgs iHoursToRespawncellCleared 480
  - set timescale to 20
5. Save game and Exit.
6. Relaunch game and goto the cell you needed reset.

[^1]: See https://forums.nexusmods.com/topic/5698852-how-to-do-a-cell-reset-that-really-works/
