# what are request water falls?

A "waterfall" refers to a sequence of network requests that depend on the completion of previous requests. 

In the case of data fetching, each request can only begin once the previous request has returned data.

This pattern is not necessarily bad. There may be cases where you want waterfalls because you want a condition to be satisfied before you make the next request. 

However, this behavior can also be unintentional and impact performance.

# Parallel data fetching

A common way to avoid waterfalls is to initiate all data requests at the same time - in parallel.

In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData() function:

By using this pattern, you can:

Start executing all data fetches at the same time, which can lead to performance gains.
Use a native JavaScript pattern that can be applied to any library or framework.
However, there is one disadvantage of relying only on this JavaScript pattern: what happens if one data request is slower than all the others?

