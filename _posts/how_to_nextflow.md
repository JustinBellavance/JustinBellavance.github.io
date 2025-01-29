---
date: '2023-12-20T11:50:54.000Z'
title: How to Write your First Nextflow Pipeline
tagline: This is the Nextflow guide I wish I had when I was starting my bioinformatics and biological data science journey.
preview: >-
    Like every up-and-coming bioinformatician, I wanted to learn Nextflow for a long time, but was pretty intimidated. As it saved a me a lot of time and stress, I really wish I learned it earlier.
image: >-
  https://repository-images.githubusercontent.com/9052236/ecd9481e-f4b3-4324-b832-a08ee1d99564
---
### Table of Contents

* Why You Should Use Nextflow
* Requirements before Starting
* Workflows
* Processes
* Configuration Files ( + a slightly more complex project)

### Why should you use Nextflow

As described on their website, Nextflow is software for “data-driven computational pipelines.” Although not only for bioinformatics, the software has seen the most success and use in this field.

[Nf-core](https://nf-co.re/pipelines), Nextflow’s “marketplace” of free, open-source premade pipelines is a goldmine of your most popular bioinformatic analyses.

That being said, Nextflow is extremely powerful for these types of analyses, and is flexible for a wide variety of cloud or local systems such as AWS, Azure, and has robust ways of handling dependencies with your software of choice, such as Docker, Singularity and/or Conda.

Last but not least, Nextflow has dependable [documentation](https://www.nextflow.io/docs/latest/index.html) supported by its populous community of users, making Nextflow quite easy to learn.

### Requirements before Starting

Before following this guide, you will need to install Nextflow.

Before that, you’ll need to make sure to have a Linux (or macOS) system. If you have Windows, look into [Ubuntu](https://ubuntu.com/) or [WSL](https://learn.microsoft.com/en-us/windows/wsl/install). They will need to have Bash installed, if not already.

Next, make sure to have Java version 11 or later installed into the previously mentioned system.

Lastly, you will need enough RAM to run Nextflow, as it can sometimes get quite intensive. I would say 8 gigabytes **at a minimum**.

Simple enough so far.

To download Nextflow itself, it’s as easy as entering the following command:

`wget -qO- https://get.nextflow.io | bash`

then,

`chmod +x nextflow `

There you have it! You are now ready to use Nextflow, as simple as that.

Although optional, a highly recommend step is to add Nextflow to your $PATH, which will make it so you can run it anywhere in your file system.

This is possible by entering this command:

`echo -e "export PATH="<your_directory>:\$PATH">> ~/.bashrc `

where <your_directory> is to be replaced by entering the value (path) printed by

`pwd `

in the directory where the _nextflow_ executable file is present.

Finally, to activate your updates without logging out and back in, you can enter

`source ~/.bashrc  `

Lastly, just enter

`nextflow -h `

in your command line to see if it works, as of December 2023, you should get an output resembling this:

![nextflow success](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*jzJMjtzui7caPYRNMJcbGA.png)

### Workflows and Running Nextflow Files.

In order to get starting with Nextflow, you need to understand two things: **Workflows** and **Processes**. Thankfully, they’re not complicated when we start out.

Workflows are where the bulk of your commands will go. If you’ve used python before, they’re essentially equivalent to:

```
if __name__ == "__main__":
  print("hello world")
```

In fact, let’s make the most simple Nextflow project possible. Create a file named _main.nf_ using your favorite text editor.

Inside, we’ll base ourselves off of our Python code above to and write:

```
  workflow {
    println "Hello World"
  }  
```

save that file, then enter in your command line:

`nextflow run main.nf  `

and you should see something like this:

![first_hello_world](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*O4G0qKwSQjlLg308by4vRA.png)

Congratulations! You’ve just ran your first Nextflow project.

If we wanted to improve on this code, it’s important to note that Nextflow is heavily based on the programming language [Groovy](https://groovy-lang.org/). All commands possible in Groovy will be possible in the workflow section of your Nextflow project. Not to mention, the Nextflow team has added some [quality-of-life functions](https://www.nextflow.io/docs/latest/script.html) to help out with common operations.

### Processes

With our basic workflow up and running, we can move on to the more complicated second half of Nextflow.

Processes can be considered the functions of your Nextflow project. You pass parameters through and expect and expect an output in return.

If we keep the same main.nf, probably our most basic Nextflow process can be written as this:

```
process HELLO_WORLD{
    "echo Hello World! > output.txt"
}  
```

This process outputs _Hello World!_ to a file called output.txt that will be found in the current directory. To run this process, we need to make some small modifications to our main.nf file. It will look like this:

```
process PRINT_HELLO_WORLD{
          output:                
            stdout        
          
          script:                
          "echo Hello world!"
}

workflow {
  PRINT_HELLO_WORLD() | view
}

```

When running our new _main.nf_ as we’ve done above, we get similar output!

![hello world nextflow](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*jqiWqu5FhPRK9psqFiLy6g.png)

As you can see, we’ve added quite a few novel things. To understand the changes, it’s important to note how processes are usually formatted.

Most often, this is how a process will look:

```  
process < name > {  
  [ directives ]  
  input:    
    < process inputs >  
    
  output:    
    < process outputs >  
    
  when:    
    < condition >  
  
  [script|shell|exec]:    
  < user script to be executed >}
```

To explain these optional definition blocks briefly:

* **Directives** are settings specific for that process. This can include the output folder, what executor to use, how much computational power to use, and what dependencies are needed. That being said, most of the options here can be specified in a good configuration file.
* **Inputs** are values given passed as a parameter by the workflow. These can be strings, integers, file paths, lists of files and more.
* **Outputs** are the values you want to keep from a process. Passing output values, which can be the same types as inputs, can make it so a future process that depends will wait until this process finishes.
* **When** (or a **condition**) is comparable to an if .. else statement that we’ve all become accustomed to. If a statement is false, it will never run the script / shell / exec command below. It’s likely to be your least used definition block, but can be useful in niche situations.
* **Script / Shell / Exec** are the workhorses of your processes. These are where the main command will be run. Most often, **Script** will be used as it is coded as a bash script of which users might be more familiar. **Shell** is useful when you are using another coding language (using a [schbang](https://bash.cyberciti.biz/guide/Shebang)) and are having a hard time using both Nextflow variables alongside your other programming language.

For example, here is a real (albeit slightly simplified) example of how I use **Shell** for my R scripts:

```  
process LOG10P_TO_P_SORT_BOTH {
      input:        
        each(step2_results)    
      
      output:        
        path("results*.regenie")    
      
      shell:    
        final_output = step2_results.getName()
        
      '''#!/usr/bin/env Rscript
      library(dplyr)
      df <- read.table("!{step2_results}", header=TRUE)
      df <- df %>%    
        mutate(P = 10 ** -(LOG10P)) %>%    
        arrange(CHROM, GENPOS)

      write.table(df, file="!{final_output}", row.names=FALSE, sep="\t", quote = FALSE)    
      '''
    }  
```

Lastly, **Exec** will allow you to run code as you might in Groovy or in the workflow, for example:

```
process simpleSum {
      input:    
        val x    
      
      exec:    p
      orintln "Hello Mr. $x"
}
```

With what we’ve covered about workflows and processes, we can already save a lot of time and struggle with Nextflow. That being said, it’s all the extra sprinkles on top that really make Nextflow a useful skill to have in your tool belt.

### Configuration Files ( + a slightly more complex project)

A good configuration file is magic. You can write far less code, simplify your pipeline and have all important settings in one fille.

To create a configuration file (also known as a _config),_ create a file named _nextflow.config_ using your editor of choice.

You can do [so many things](https://www.nextflow.io/docs/latest/config.html) in your config, it would be impossible to name them all. For simple scripts, here are some of the most useful.

You can **define variables**. This can take form of files, directories, strings, integers, lists, etc.. For example, you can define an **outDir**, where your files will be copied upon a process finishing.

These variables can be **scoped,** meaning that some variables can be exclusive to some processes - if named properly.

You can also set **global options**, like things such as _dag.enabled_ to create a diagram of your pipeline or notification.to to send an email upon job completion (with some additional settings), just to name a few.

Below is a config file that includes everything we’ve spoken about so far. We will be using it with our final pipeline later in this guide.

main.nf:

``` 
process PRINT_HELLO_WORLD{
          label "simple_message"
          publishDir "$params.OutDir/output"

          input:                
            val(message)    

          output:                
            val("output.txt") 

          script:                
          "echo $message \$TIMES > output.txt"
}

workflow {        
  PRINT_HELLO_WORLD(params.message)
}  
          ```

nextflow.config:

```
dag.enabled = true
params { 
         OutDir= "/home/justi"        
         message = "Hello World!"
         }

process {        
  withLabel : "simple_message"  { 
    beforeScript = "export TIMES=x5"
                    cpus = 1
                    time = "1h"
                    memory = "4GB"
  }
}
```


In the command line, we simply enter the usual:

`nextflow run main.nf`

... and voila!

Lastly, if you’re not running locally, you can easily define parameters for allocating computational resources such as time, memory and nodes for AWS, Azure, Google Cloud and more.

#### Conclusion

Nextflow is an extremely powerful tool to upgrade your pipeline workflow.

If not already, I highly encourage you to dive in, learn, make mistakes and upgrade your bioinformatic analysis.

Justin
