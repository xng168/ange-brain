# Diagnosed gbrain PGLite Database Lock Issue

- **Investigated database lock error** preventing `gbrain import` from running
- **Found root cause**: A live `gbrain serve` process (MCP server, PID 24636) was holding an exclusive write lock on the PGLite database — PGLite only allows one writer at a time, causing contention
- **Verified lock was active**: Confirmed the lock file showed current heartbeat timestamp, not stale; the bun.exe process was actively running
- **Identified the solution**: Either kill the background server temporarily to run the import, or restart the Claude Code session (which will spawn a fresh server)
- **Not data corruption**: The database itself is fine; it's just process contention requiring a brief restart or session reload to resolve
