https://www.redhat.com/en/blog/modernization-developing-your-code-migration-strategy

If the code is being changed, the following two strategies can provide lots of benefits:

1. Make the code more testable and write tests
2. Update the code and configuration to be more container friendly

Fowler defines refactoring as, “change made to the internal structure of software to make it easier to understand and cheaper to modify without changing the observable behavior.” 

### Mocking can help deal with entanglement

Mocking - create objects that mimic the behavior of real objects

If you mock all functionality related to downstream service operations, including simulating potential outputs, good and bad, the database can still blow up—however, if you have done your mocking and testing well, you will at least know your code can handle it.

[The Twelve-Factor App](https://12factor.net/) is a very useful methodology for building easy-to-change software. Following these factors can guide developers in building code that can run in any environment (including containers).

However, it should be noted that trying to follow all twelve factors is unrealistic, especially when it comes to legacy code. You can follow the factors enough to get your application closer to its future state and to be able to iterate on both the product and operations loops.