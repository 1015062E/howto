<br>
<table>
  <td>WARNING</td>
  <td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

*Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.*

## Understanding DirectQuery in Power BI

Power BI’s DirectQuery mode enables real-time querying of external data sources, such as SQL databases, without importing data into the platform’s memory. Two critical settings govern DirectQuery performance: **Max DirectQuery Parallelism** and **Max Concurrent DirectQuery Connections (per semantic model)**. These settings, particularly relevant for Power BI Premium capacities like the F64 SKU, can significantly impact report performance and scalability. This post demystifies these concepts for beginners, using simple explanations and examples, and addresses common questions about their configuration.

### What is DirectQuery?

DirectQuery allows Power BI to send queries directly to an external data source, retrieving results in real-time. Unlike importing data into Power BI’s in-memory engine, DirectQuery keeps data at the source, which is ideal for large datasets or scenarios requiring up-to-date information. However, this approach depends heavily on the data source’s performance and Power BI’s ability to manage queries efficiently.

### Key Concepts: Parallelism and Connections

To understand DirectQuery performance, we need to explore two settings:

#### Max DirectQuery Parallelism

**Max DirectQuery Parallelism** determines the maximum number of queries Power BI can send to the data source simultaneously for a single semantic model (dataset). This setting enhances report performance by allowing multiple queries—such as those for different visuals in a dashboard—to execute concurrently.

- **Default and Maximum**: For the F64 SKU, parallelism ranges from 4 (default) to 8 (maximum), adjustable via the `Model.MaxParallelismPerQuery` property.
- **Purpose**: Parallelism reduces report load times by processing queries simultaneously rather than sequentially.

**Example**: Consider a Power BI report with four visuals: a sales chart, a customer table, a profit trend, and a product breakdown. Each visual requires a query to a SQL database. With parallelism set to 4, Power BI can send all four queries at once, making the report load faster. If parallelism were limited to 1, queries would process one at a time, slowing the experience.

#### Max Concurrent DirectQuery Connections

**Max Concurrent DirectQuery Connections (per semantic model)** defines the maximum number of simultaneous connections Power BI can establish to the data source for a semantic model. Each connection is an open channel for sending queries and retrieving results.

- **Limit**: For the F64 SKU, the maximum is 50 connections.
- **Purpose**: This setting ensures the data source can handle multiple interactions without being overwhelmed, supporting multiple users or complex reports.

**Example**: If 10 users access a semantic model, each viewing a report with 5 queries (50 queries total), 50 connections allow Power BI to manage these interactions efficiently, even if only 8 queries run simultaneously due to parallelism limits.

### Why Are There More Connections Than Parallel Queries?

A common question arises with the F64 SKU configured to its maximum values: **Max DirectQuery Parallelism = 8** and **Max Concurrent DirectQuery Connections = 50**. If only 8 queries can run at once, why are 50 connections needed? Isn’t this a waste of 42 connections?

#### Understanding the Relationship

- **Parallelism** governs how many queries can execute simultaneously, typically requiring one connection per query during parallel execution. With parallelism at 8, up to 8 connections may be active for those queries.
- **Connections** represent the total pool of channels available for all queries, including those from multiple users, sequential queries, or connection pooling for efficiency.

#### Why 50 Connections Are Necessary

Setting connections to 8 might seem sufficient for 8 parallel queries, but this limits scalability:

- **Multiple Users**: In an organization, multiple users may access the same semantic model simultaneously. With 50 connections, Power BI can support many users without delays, whereas 8 connections could bottleneck access.
- **Complex Reports**: A report with more than 8 visuals may generate additional queries processed sequentially. Extra connections allow these queries to be handled efficiently.
- **Connection Pooling**: Power BI reuses connections to avoid the overhead of opening/closing channels. A larger pool (50) ensures flexibility during peak demand.

#### Are Extra Connections Wasteful?

The 42 “extra” connections are not wasted. They provide:

- **Scalability**: Support for enterprise-scale workloads with many users or reports.
- **Flexibility**: Readiness for spikes in demand without performance degradation.
- **Optimization**: Alignment with the data source’s ability to handle multiple connections, maximizing efficiency.

In practice, Power BI uses only the connections needed at any moment, so the 50-connection limit is a resource pool, not a fixed allocation.

### Practical Implications for Power BI Users

For users managing an F64 capacity:

- **Optimize Parallelism**: If reports are slow, consider increasing `Model.MaxParallelismPerQuery` from 4 to 8, provided the data source supports concurrent queries. Consult your database administrator to confirm compatibility.
- **Leverage Connections**: The 50-connection limit is fixed and designed for enterprise use. It ensures robust performance without manual tuning.
- **Monitor Performance**: Use tools like the Microsoft Fabric Capacity Metrics app (when available) to track resource usage and adjust settings as needed.

### Conclusion

Understanding **Max DirectQuery Parallelism** and **Max Concurrent DirectQuery Connections** is key to optimizing Power BI DirectQuery performance. Parallelism (e.g., 8 for F64) speeds up reports by processing multiple queries simultaneously, while connections (e.g., 50) provide the infrastructure for scalability and efficiency. Far from being wasteful, a larger connection pool enhances flexibility and performance, making Power BI a powerful tool for enterprise reporting.
