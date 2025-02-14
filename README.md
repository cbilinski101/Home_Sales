# Home Sales Analysis

## Dependencies

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-Enabled-orange)
![Google Colab](https://img.shields.io/badge/Google%20Colab-Supported-yellow)
![Pandas](https://img.shields.io/badge/Pandas-Enabled-lightblue)
![PySpark](https://img.shields.io/badge/PySpark-Enabled-red)

## Overview

This project analyzes home sales data using Python and Google Colab. The **Home_Sales.ipynb** file contains data processing, visualization, and statistical insights related to housing sales trends. The analysis includes partitioned Parquet files, cached data, and structured tables for optimized performance.

## Features

- Data Cleaning & Preprocessing
- Exploratory Data Analysis (EDA)
- Correlation & Pivot Table Analysis
- Visualizations of Housing Trends
- Partitioned Parquet Data Handling
- Cached Data for Efficient Processing

## Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/your-username/your-repo-name.git
   ```
2. Navigate to the project directory:
   ```sh
   cd your-repo-name
   ```
3. Open Google Colab and upload the **Home_Sales.ipynb** notebook.

## Usage

1. Open Google Colab: [Google Colab](https://colab.research.google.com/)
2. Upload **Home_Sales.ipynb** to your Google Drive.
3. Open the notebook and run the cells sequentially to perform the analysis.

## Data Handling

- **Partitioned Parquet Files**: The dataset is stored in partitioned Parquet format for efficient querying and processing.
- **Cached Data**: Intermediate results are cached to speed up computations and reduce redundant processing.
- **Tables**: Structured tables are used to organize and analyze data efficiently.

## Performance Comparison

### Query Execution Times

| Query Type         | Runtime (seconds) |
|--------------------|------------------|
| **Uncached Query** | 1.087            |
| **Cached Query**   | 0.570            |
| **Parquet Query**  | 1.368            |

### Observations

1. **Using Cached Data** significantly reduces execution time compared to the uncached query (from **1.087s to 0.570s**, a **~47% improvement**).
2. **Using Parquet Data** is slightly slower (**1.368s**) than the uncached query. This is likely due to the overhead of reading Parquet files before computation.

### Key Takeaways

- **Parquet without Partitioning:** Since `view` wasn't used as a partition column, the query had to scan the entire dataset instead of leveraging partition pruning, leading to a **slower** execution.
- **Caching Benefits:** Cached data (**0.570s**) significantly improved performance because Spark stored the frequently accessed data in memory, avoiding disk I/O.
- **Partitioning Optimization:** If `view` were a partition column in the Parquet dataset, Spark could have **skipped unnecessary partitions**, potentially making the query **faster** than both the uncached and cached versions.

### Next Steps

- **Consider partitioning the Parquet dataset on `view`** if queries frequently filter or group by it.
- **Use caching for repeated queries** when working with in-memory dataframes for quick lookups.
- **Analyze execution plans (`explain()` in Spark SQL)** to see where optimizations can be applied.

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature-name`
3. Commit changes: `git commit -m 'Add feature'`
4. Push to the branch: `git push origin feature-name`
5. Open a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
