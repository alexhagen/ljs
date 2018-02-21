# ljs - Long Job Scheduler

There's a million job schedulers out there right now, but most of them focus
on short jobs - little millisecond computations that you need to offload as
easily as possible.  You don't want to fiddle with when to run those. But what
I need is long job scheduling - I run 30 hour simulations pretty often.  There
are a couple packages out there that I find useful, such as ``schedule`` and
``ray`` for Python.  This package seeks to combine and extend these two
packages and give a toolset for scheduling of long jobs.

## Feature Set

- [ ] Scheduling a'la ``schedule``
```python
ljs.tonight().do(job)
```
- [ ] Remoting a'la ``ray``
```python
@ljs.remote
def job():
  print("working");

ljs.tonight().do(job)
```
- [ ] Remoting with specific requirements
```python
@ljs.remote(num_gpus=1)
def deep_learning_job():
  print("categorizing puppies")

@ljs.remote(num_cpus=4)
def simulation_job():
  print("monte carlo simulations requiring a lot of cores")
```
- [ ] *Chaining* of commands
```python
def job_1():
  print("creating data for job 2")

def job_2():
  print("doing work depending on data from job 1")

ljs.tonight().do(job_1)
ljs.after(job_1).do(job_2)
```
- [ ] A job dashboard (theme https://github.com/puikinsh/gentelella)
- [ ] A ``jupyter`` widget replacing deferred jobs
- [ ] A ``jupyter`` magic for "depends" - finding jobs that depend on a file
  and waiting until that file appears - can use a time estimate or
  "expeonential backoff"
- [ ] A ``jupyter`` magic for "track" - watches the output of a file and
  decides, depending on time, size of file, or certain strings in the file
  how much progress has been made - polling methodology
