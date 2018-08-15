# Performing code instrumentation with Clover (OpenClover) and AspectJ

[Clover](https://openclover.org/) is a code coverage tool originally owned by Atlassian and afterwards open-sourced. AspectJ is a framework for Aspect-Oriented Programming. Both of these frameworks mess up with the source code, and from what I experience this can be troublesome. The following lists how we can make these work without any problems and provides three alternative ways for changing your plugins to achieve this same goal:

1. `maven-compiler-plugin` must not try to recompile already compiled code from `aspectj-maven-plugin`, therefore AspectJ compiler goals are run in `process-sources` phase;
2. Both OpenClover and AspectJ add source code to each method, and therefore AspectJ may raise an unexpected code error. In order for this to work, one of three methods may be implemented:

   1. Inline all `@Pointcut` definitions so that OpenClover doesn't add any coverage code to an empty method body;
   2. Aspect files can be excluded from code coverage using `<exclude>..</exclude>` configuration in `clover-maven-plugin`. This is the solution adopted in this example;
   3. Aspect files can also be renamed from `*.java` to `*.aj`, making OpenClover simply ignore the latter. This is the easiest solution;
  
  
Also, original StackOverflow question: https://stackoverflow.com/questions/50744732/openclover-getting-to-work-with-aspectj
