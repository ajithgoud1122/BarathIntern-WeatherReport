import csv
import random
import matplotlib.pyplot as plt
import pandas as pd
from datetime import datetime, timedelta



start_date = datetime(2023, 9, 15)
end_date = datetime(2023, 10, 15)
date_range = [start_date + timedelta(days=x) for x in range((end_date - start_date).days + 1)]

weather_data = []

for date in date_range:
    for _ in range(4):  # Four data points per day at different times
        time = random.choice(["Morning", "Afternoon", "Evening", "Night"])
        temperature = round(random.uniform(30, 39), 2)  # Random temperature between 10 and 30 degrees Celsius
        status = random.choice(["Sunny", "Cloudy", "Rainy"])

        weather_data.append({
            "date": date.strftime("%Y-%m-%d"),
            "day": date.strftime("%A"),
            "time": time,
            "temperature": temperature,
            "status": status,
            "month": date.strftime("%B"),
        })


csv_file_path = "weather_data.csv"
csv_columns = ["date", "day", "time", "temperature", "status", "month"]

with open(csv_file_path, 'w', newline='') as csvfile:
    writer = csv.DictWriter(csvfile, fieldnames=csv_columns)
    writer.writeheader()
    for data in weather_data:
        writer.writerow(data)


# Read data from CSV file
df = pd.read_csv(csv_file_path)

# Plot 1: Date vs Temperature
plt.figure(figsize=(10, 6))
plt.plot(df['date'], df['temperature'], marker='o')
plt.title('Date vs Temperature')
plt.xlabel('Date')
plt.ylabel('Temperature (°C)')
plt.xticks(rotation=45)
plt.grid(True)
plt.show()

# Plot 2: Status vs Temperature
plt.figure(figsize=(8, 5))
df.boxplot(column='temperature', by='status')
plt.title('Status vs Temperature')
plt.suptitle('')  # Remove default title
plt.xlabel('Status')
plt.ylabel('Temperature (°C)')
plt.show()

# Plot 3: Date vs Status
plt.figure(figsize=(10, 6))
df.groupby(['date', 'status']).size().unstack().plot(kind='bar', stacked=True)
plt.title('Date vs Status')
plt.xlabel('Date')
plt.ylabel('Count')
plt.xticks(rotation=45)
plt.show()

# Plot 4: Pie chart on Status only
status_counts = df['status'].value_counts()
plt.figure(figsize=(8, 8))
plt.pie(status_counts, labels=status_counts.index, autopct='%1.1f%%', startangle=90)
plt.title('Distribution of Weather Status')
plt.show()
