import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.patches import FancyArrowPatch

# Data from the provided table
data = {
    'Model': ['RF', 'Xg Boost'],
    'MSE': [0.0044, 0.0059],
    'MAE': [0.0490, 0.0619],
    'RMSE': [0.0668, 0.0772],
    'R2': [0.8734, 0.8312]
}

df = pd.DataFrame(data)

# Setting up the figure and axes
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 6))

# Set background color for subplots to white
ax1.set_facecolor('white')
ax2.set_facecolor('white')

# Colors for the bars
colors = ['#8A2BE2', '#DC143C', '#FFD700']  # Colors for MSE, MAE, RMSE
r2_color = '#2E8B57'  # Color for R^2

# Bar width
width = 0.25

# Plotting MSE, MAE, RMSE on the first axes
x = np.arange(len(df['Model']))  # the label locations
for i, metric in enumerate(['MSE', 'MAE', 'RMSE']):
    ax1.bar(x + i*width, df[metric], width, label=metric, color=colors[i])

# Setting labels with appealing color
ax1.set_xlabel('Models', color='black')
ax1.set_ylabel('Values')
ax1.set_xticks(x + width)
ax1.set_xticklabels(df['Model'], color='black')
ax1.legend()

# Ensuring the axes are clearly defined
ax1.spines['bottom'].set_linewidth(2)
ax1.spines['left'].set_linewidth(2)

# Configuring grid lines
ax1.yaxis.grid(True, color='black', linestyle='-', linewidth=0.5, alpha=0.5)
ax1.grid(axis='x', visible=False)

#Adjusting the y-axis scale for clearer visibility of MSE, MAE, RMSE values
ax1.set_ylim(0.0,1.0)  #Adjust this range based on your minimum R2 value to maximize visibility

# Plotting R^2 on the second axes, with appropriate bar width
ax2.bar(x, df['R2'], width, label='R$^2$', color=r2_color)
ax2.set_xlabel('Models', color='black')
ax2.set_ylabel('R$^2$ Value')
ax2.set_xticks(x)
ax2.set_xticklabels(df['Model'], color='black')
ax2.legend()

# Adjusting the y-axis scale for clearer visibility of R^2 values
ax2.set_ylim(0.4, 1)  # Adjust this range based on your minimum R2 value to maximize visibility

# Ensuring the axes are clearly defined
ax2.spines['bottom'].set_linewidth(2)
ax2.spines['left'].set_linewidth(2)

# Configuring grid lines
ax2.yaxis.grid(True, color='black', linestyle='-', linewidth=0.5, alpha=0.5)
ax2.grid(axis='x', visible=False)

# Overall title across both subplots
fig.suptitle('Metrics Comparison (MSE, MAE, RMSE, R$^2$) for Density', fontsize=16)

# Layout adjustments
plt.tight_layout(rect=[0, 0, 1, 0.95])  # Adjust layout to make space for the central title

plt.show()

