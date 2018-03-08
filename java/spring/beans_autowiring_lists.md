[Java](https://github.com/laurenzfiala/wiki/tree/master/java) > [Spring](https://github.com/laurenzfiala/wiki/tree/master/java/spring)

## Bean Autowiring Lists

When `@Autowire`-ing a bean which returns an array of e.g. Interfaces, the bean will actually NOT be used, instead if there are beans fitting for the interface, Spring will use these beans and populate an array internally with all found matching beans.

### Usecases

- When `@Autowire`-ing any object array

### What to do

Construct the array in the bean of the containing class instead of `@Autowire`-ing the array bean.