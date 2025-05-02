from pyspark.sql import SparkSession

# Create Spark session
spark = SparkSession.builder.appName("Data Cleaning").getOrCreate()

# Load your CSV file
df = spark.read.option("header", True).option("inferSchema", True).csv("big_data.csv")

# Show schema and sample
print("Original Data:")
df.printSchema()
df.show(5)

# Drop rows where all values are null
df = df.dropna(how='all')

# Remove duplicate rows
df = df.dropDuplicates()

# Save the cleaned data
df.write.option("header", True).csv("cleaned_output")

print("Data cleaning completed. Cleaned data saved to 'cleaned_output' folder.")

# Stop session
spark.stop()

