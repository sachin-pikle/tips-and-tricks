# How to clone a child folder (and it's subfolders) from GitHub

***Credits: @RahulMR42 Rahul's code snippet:
https://github.com/oracle-devrel/oci-devops-examples/tree/main/oci-coderepo-examples/oci-devops-coderepo-with-github***


Like several sample code repositories, the [oci-devops-examples](https://github.com/oracle-devrel/oci-devops-examples) code repository consists of several standalone examples, each in its own child folder (and subfolders) inside the repository. 

Say, we need to clone just a single example [oci-devops-coderepo-with-github](https://github.com/oracle-devrel/oci-devops-examples/tree/main/oci-coderepo-examples/oci-devops-coderepo-with-github) located in:
```
oci-devops-examples >> oci-coderepo-examples >> oci-devops-coderepo-with-github
```

We can achieve it with the following set of commands:

``` shell
git init oci-devops-coderepo-with-github

cd oci-devops-coderepo-with-github

git remote add origin https://github.com/oracle-devrel/oci-devops-examples

git config core.sparsecheckout true

echo "oci-coderepo-examples/oci-devops-coderepo-with-github/*">>.git/info/sparse-checkout

git pull --depth=1 origin main
```

Similarly, the [oracle-functions-samples](https://github.com/oracle-samples/oracle-functions-samples) repository also has a collection of function samples, each in its own folder (and subfolders) inside the repository. 

Let's apply the above tip to clone just the [trace-functions-with-apm](https://github.com/oracle-samples/oracle-functions-samples/tree/master/samples/trace-functions-with-apm) sample from this repository located in:

```
oracle-functions-samples >> samples >> trace-functions-with-apm
```

We can achieve it with the following set of commands:

``` shell
git init trace-functions-with-apm

cd trace-functions-with-apm

git remote add origin https://github.com/oracle-samples/oracle-functions-samples

git config core.sparsecheckout true

echo "samples/trace-functions-with-apm/*">>.git/info/sparse-checkout

git pull --depth=1 origin master
```