# Create

- CodeBuild
- Create
- Choose source
- Recommended to use Ubuntu environment
	- Standard
	- Latest
- Buildspec
	- Default looks for buildspec.yml
- Confirm

- Start build

# Example buildspec.yml

- Part of the test is to check that "congratulations" is in the index.html file

```yml
version: 0.2

phases: 
    install:
        runtime-versions:
            nodejs: latest
        commands:
            - echo "installing something"
    pre_build:
        commands: 
            - echo "we are in the pre build phase"
    build:
        commands:
            - echo "we are in the build block"
            - echo "we will run some tests"
            - grep -Fq "Congratulations" index.html
    post_build:
        commands:
            - echo "we are in the post build phase"
```

