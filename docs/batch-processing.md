# Batch Processing (Spring Framework).

* To `batch` is the act of arranging things in groups.
* A `batch` is a quantity coming or taken at one time.
* `Batch processing` (in computing) is the scripted running of one or more tasks.

### Concepts

#### A job.

A `Job` is an entity that encapsulates an entire batch process.

A job should:
* Have a simple name.
* Define steps and their order.
* Define whether the job can be restarted.

#### A job instance.

In spring, a `JobInstance` refers to the concept of a logical job run. The implementation of a job instance has no understanding of the data to be loaded. `ItemReader`s provide the logic for loading data.

#### Job parameters.

A `JobParameters` object holds a set of parameters used to start a batch job. Job parameters help in distinguishing a job instance from another.

> Not all job parameters are required to contribute to the identification of a JobInstance. By default, they do so. 
> However, the framework also allows the submission of a Job with parameters that do not contribute to the identity of a JobInstance.

#### A job execution.

A `JobExecution` is a single attempt to run a job. Job executions can fail/succeed. The `JobInstance` corresponding to a certain job execution is only considered successful if the job execution ends successfully.

> A Job defines what a job is and how it is to be executed, and a JobInstance is a purely organizational object to group executions together, primarily to enable correct restart semantics. A JobExecution, however, is the primary storage mechanism for what actually happened during a run and contains many more properties that must be controlled and persisted.

#### A step.

A `Step` is a Spring domain object that describes a single, sequantial phase of a batch `Job`. Hence, each job is made up of one or more steps. 

#### A step execution.

In Spring, a `StepExecution` is a single attempt to execute a `Step`.

>  A new `StepExecution` is created each time a `Step` is run, similar to `JobExecution`. However, if a step fails to execute because the step before it fails, no execution is persisted for it. A `StepExecution` is created only when its Step is actually started.

#### An execution context.

An `ExecutionContext` is store of key/value state data (managed by the Spring framework) scoped to a `JobExecution` or `StepExecution` instance.

#### A job repository.

A `JobRepository` is a data persistence mechanism used by all Spring stereotypes described above.

> It provides CRUD operations for `JobLauncher`, `Job`, and `Step` implementations. When a `Job` is first launched, a `JobExecution` is obtained from the repository, and, during the course of execution, `StepExecution` and `JobExecution` implementations are persisted by passing them to the repository.

Use `@EnableBatchProcessing` to configure a `JobRepository` automatically.

#### A job launcher.

A `JobLauncher` is an interface for running jobs given a set of parameters.

#### An item reader.

An `ItemReader` is an interface that represents the retrieval of input for a `Step`.

#### An item writer.

An `ItemWriter` is an abstraction that represents the output of a Step, one batch or chunk of items at a time.

#### An item processor.


