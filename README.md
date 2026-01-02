# K-Means RFM Customer Segmentation Analysis

A ready-to-use Python template for performing customer segmentation using K-Means clustering on RFM (Recency, Frequency, Monetary) metrics.

## What is RFM Analysis?

RFM analysis is a proven marketing technique used to segment customers based on their purchasing behavior:

- **Recency (R)**: How recently did the customer make a purchase? (measured in days)
- **Frequency (F)**: How often do they purchase? (number of unique orders)
- **Monetary (M)**: How much money do they spend? (total revenue)

By clustering customers using these three metrics, you can identify distinct customer segments (e.g., high-value customers, at-risk customers, dormant customers) and tailor marketing strategies accordingly.

## Features

- Step-by-step Jupyter notebook with clear documentation
- Automated RFM metric calculation
- Elbow method for determining optimal cluster count
- Outlier detection with boxplot visualizations
- Customizable cluster naming
- Export results to CSV and Excel formats

## Prerequisites

Before using this template, ensure you have Python installed (Python 3.7 or higher recommended).

## Installation

1. Clone or download this repository:
```bash
git clone https://github.com/yourusername/kmeans-rfm-analysis-python.git
cd kmeans-rfm-analysis-python
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

## Input Data Requirements

### Data Format

Your input data should be a CSV file with **one row per order** containing the following columns:

| Column | Description | Data Type | Example |
|--------|-------------|-----------|---------|
| `cust_id` | Customer ID | String/Integer | 1001, CUST_A |
| `date` | Order date | Date | 2024-01-15 |
| `ordnum` | Order number (must be unique per order) | String/Integer | ORD001, 12345 |
| `rev` | Revenue amount | Numeric | 150.50, 299.99 |

### Example CSV (semicolon-delimited, comma as decimal):
```csv
cust_id;date;ordnum;rev
1001;2024-01-15;ORD001;150,50
1001;2024-03-20;ORD002;75,25
1002;2024-02-10;ORD003;299,99
1003;2024-01-05;ORD004;50,00
```

### Recommendations

- **Time Period**: Use 6-24 months of historical order data for meaningful results
- **Data Quality**: Ensure order numbers are unique and revenue values are positive
- **CSV Format**: The default format uses semicolon (`;`) as delimiter and comma (`,`) as decimal separator. Adjust in the code if your format differs.

## Usage Guide

### Step 1: Prepare Your Data

Place your CSV file in an accessible location and note the file path.

### Step 2: Import and Configure

Open [kmeans_clustering_script.ipynb](kmeans_clustering_script.ipynb) and update the file path in section 1:

```python
# TODO: Replace "LOCATION/FILE.csv" with your actual file path
data = pd.read_csv("data/customer_orders.csv", delimiter=";", decimal=",")
```

### Step 3: Run Data Processing

Execute sections 1 and 2 to:
- Load and filter your data (removes orders with revenue ≤ 0)
- Calculate RFM metrics for each customer

### Step 4: Determine Optimal Clusters

Run section 3 to generate the elbow plot. Look for the "elbow point" where the curve begins to flatten - this suggests the optimal number of clusters.

![Elbow Method Example](https://via.placeholder.com/600x400?text=Elbow+Plot+Example)

### Step 5: Perform Clustering

In section 4, update `n_clusters` with your chosen number:

```python
# TODO: Insert the optimal number of clusters based on the elbow plot above
kmeans_basic = KMeans(n_clusters=3, random_state=1234).fit(data_rfm_elbow)
```

Run section 4 and review the `kmeans_basic_centers` output to understand each cluster's characteristics.

### Step 6: Analyze Outliers

Run section 5 to visualize boxplots for each RFM metric by cluster. Identify if extreme outliers are affecting your clustering and consider filtering them if necessary.

### Step 7: Name Your Clusters

In section 6, customize cluster names based on the characteristics you observed:

```python
cluster_name_mapping = {
    0: 'VIP Customers',      # Low recency, high frequency, high monetary
    1: 'At Risk',            # High recency, medium frequency, medium monetary
    2: 'Lost Customers'      # Very high recency, low frequency, low monetary
}
```

### Step 8: Export Results

Update the export path in section 7 and run to save your results:

```python
data_rfm_with_cust_id.to_csv('output/data_rfm.csv', index=False)
data_rfm_with_cust_id.to_excel('output/data_rfm.xlsx', index=False)
```

## Output

The final output includes:

- **data_rfm.csv / data_rfm.xlsx**: Customer-level data with RFM metrics and assigned cluster labels
- **Cluster centers**: Mean RFM values for each cluster segment
- **Visualizations**: Elbow plot and boxplots for analysis

### Example Output Structure

| cust_id | frequency | recency | monetary | Cluster |
|---------|-----------|---------|----------|---------|
| 1001 | 5 | 30 | 1250.50 | VIP Customers |
| 1002 | 2 | 180 | 350.00 | At Risk |
| 1003 | 1 | 365 | 50.00 | Lost Customers |

## Customization Tips

### Adjusting for Different Data Formats

If your CSV uses different delimiters or decimal separators:

```python
# Example: Standard CSV (comma-delimited, period as decimal)
data = pd.read_csv("data/orders.csv", delimiter=",", decimal=".")
```

### Testing More Cluster Options

Increase the range in the elbow method:

```python
wss = calculate_wss(data_rfm_elbow, 10)  # Test up to 10 clusters
plt.plot(range(1, 11), wss, ...)
```

### Adding Data Scaling (Advanced)

K-Means can be sensitive to scale differences. If monetary values are much larger than recency/frequency, consider scaling:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
data_rfm_scaled = scaler.fit_transform(data_rfm[['recency', 'frequency', 'monetary']])
```

## Troubleshooting

**Issue**: "FileNotFoundError: [Errno 2] No such file or directory"
- **Solution**: Check that your file path is correct and use forward slashes (`/`) or escaped backslashes (`\\`) in Windows paths

**Issue**: Clusters seem unbalanced (one cluster has most customers)
- **Solution**: Try a different number of clusters or consider scaling your data

**Issue**: "ParserError: Error tokenizing data"
- **Solution**: Verify your CSV delimiter and decimal separator settings match your file format

**Issue**: Elbow plot doesn't show a clear elbow
- **Solution**: This is normal for some datasets. Choose a number of clusters that balances interpretability and distinctiveness (typically 3-5 clusters)

## Contributing

Contributions are welcome! Feel free to:
- Report bugs or issues
- Suggest improvements or new features
- Submit pull requests

## License

This project is open source and available under the MIT License.

## Acknowledgments

This template is designed for educational and commercial use. RFM analysis is a widely-used technique in customer analytics and marketing.

## Contact

For questions or feedback, please open an issue in this repository.

---

**Happy Clustering!** Use these insights to better understand your customers and optimize your marketing strategies.
