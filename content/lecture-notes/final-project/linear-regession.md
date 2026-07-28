Sure, here is a simple Python script using linear regression from the `sklearn` library to predict next month’s expenses based on the previous three months. This script assumes that you have your expenses data in a list where each element represents the expenses of a month.

```python
from sklearn.linear_model import LinearRegression
import numpy as np

# Your expenses for the last three months (for example)
expenses = [200, 220, 250]

# Reshape the data
X = np.array(range(len(expenses))).reshape(-1, 1)
y = np.array(expenses).reshape(-1, 1)

# Create and train the model
model = LinearRegression()
model.fit(X, y)

# Predict next month's expenses
next_month = len(expenses)
predicted_expenses = model.predict(np.array([next_month]).reshape(-1, 1))

print(f"Predicted expenses for the next month: {predicted_expenses[0][0]}")
```

Please note that this is a very basic model and might not give very accurate predictions. For more accurate predictions, you might want to consider more complex models and more features (like the month of the year, special events, etc.). Also, remember to use a larger dataset for training the model for real-world applications. This script is just a starting point. You would need to adjust it according to your specific needs.

Also, please make sure to install the necessary Python libraries by running `pip install numpy sklearn` in your terminal before running the script. If you’re using a Jupyter notebook, you can run this command directly in a code cell by prefixing it with an exclamation mark like this: `!pip install numpy sklearn`.

Let me know if you need help with anything else! 😊