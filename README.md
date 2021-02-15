# Duper

This project is written to find duplicate files on a given directory. This purpose is achieved by a collaborative work of some servers set on main supervisor: called Duper.Application:

- Results -> It keeps records of already run files. It keeps the state of the application by holding a Map of hashes as keys and its values being a list of duplicate file names
- PathFinder -> It runs based on DirWalker hex package to traverse file in the set directory
- Gatherer -> It kicksoff the amount of workers (managed by a proper OTP Supervisor) according to a given number and presents (calling Results server) the list of duplicated results once all workers have finished their jobs
- WorkerSupervisor -> It's a DynamicSupervisor to handle creation of a GenServer server (Worker) by a request
- Worker -> it properly check a file content by opening a stream and hashing (md5) its content to be used as a comparisson mechanism. It uses event message (or callbacks) to let Gatherer server know that it is available to receive next file to do its job. Next file is retrieved by asking PathFinder


## Running

- Have elixir tool installed: mix (it comes with elixir standard installation)
- Clone the project and inside of it run `mix run --no-halt` to see a list having lists of duplicate file paths

### Some notes

- By this commit, the current directory is set for `~` (`home` in unix operating systems). It can be manually changed on `lib/duper/application.ex`
- A amount of 25 workers is set on `lib/duper/application.ex`.

---

- This project is written based on Programming Elixir >= 1.6 book by Dave Thomas through Pragprog
