# Can a single image in OCIR have multiple tags?

The answer is yes. A single image in OCIR can have multiple tags.

We can achieve it with the following set of commands:

1. Pull an image you wish to add multiple tags to.

    ``` shell
    docker pull phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:qug3cic
    ```

2. Check the image details.

    ``` shell
    docker images -a
    ```
    
    The output should look like the following:
    
    ``` shell
    REPOSITORY                                                        TAG                 IMAGE ID            CREATED             SIZE
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   qug3cic             079d547efd6c        23 minutes ago      91.2MB
    ```

3. Tag the image with other tags.

    ``` shell
    docker image tag 079d547efd6c phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:latest
    
    docker image tag 079d547efd6c phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1.0.1-b1
    
    docker image tag 079d547efd6c phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1.0.1
    
    docker image tag 079d547efd6c phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1.0
    
    docker image tag 079d547efd6c phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1
    ```

4. Check the image details.

    ``` shell
    docker images -a
    ```
    The output should look like the following. Note the IMAGE ID is the same for all the tags.
    
    ``` shell
    REPOSITORY                                                        TAG                 IMAGE ID            CREATED             SIZE
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   latest              079d547efd6c        57 minutes ago      91.2MB
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   qug3cic             079d547efd6c        57 minutes ago      91.2MB
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   v1                  079d547efd6c        57 minutes ago      91.2MB
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   v1.0                079d547efd6c        57 minutes ago      91.2MB
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   v1.0.1              079d547efd6c        57 minutes ago      91.2MB
    phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17   v1.0.1-b1           079d547efd6c        57 minutes ago      91.2MB
    ```

5. Push the image with all the tags to OCIR.

    ``` shell
    docker push phx.ocir.io/my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17
    ```
    This command pushes all the tags to OCIR.

6. To verify, login to the OCI Console. Go to `Developer Services >> Containers & Artifacts >> Container Registry` in your compartment. Go to the image in the repository `gvm/jibber-ni-gvmce22-jdk17` and click on `Associated Tags`. You should see all the tags:

    ``` shell
    Tag	        Full path
    qug3cic	    my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:qug3cic
    v1.0.1-b1	my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1.0.1-b1
    v1	        my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1
    v1.0	    my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1.0
    v1.0.1	    my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:v1.0.1
    latest	    my-tenant-namespace/gvm/jibber-ni-gvmce22-jdk17:latest
    ```
