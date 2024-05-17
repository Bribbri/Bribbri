import numpy as np
import scipy.stats as stats
import matplotlib.pyplot as plt

def plot_t_test(t_stat, df, alpha, tail='two'):
    x = np.linspace(-4, 4, 1000)
    y = stats.t.pdf(x, df)
    
    plt.plot(x, y, label='t-distribution')
    
    if tail == 'two':
        t_critical = stats.t.ppf(1 - alpha / 2, df)
        plt.fill_between(x, y, where= (x < -t_critical) | (x > t_critical), color='red', alpha=0.5)
        plt.axvline(t_stat, color='blue', linestyle='--', label=f't-statistic: {t_stat:.2f}')
        plt.axvline(-t_critical, color='green', linestyle='--', label=f'Critical values: ±{t_critical:.2f}')
        plt.axvline(t_critical, color='green', linestyle='--')
    elif tail == 'left':
        t_critical = stats.t.ppf(alpha, df)
        plt.fill_between(x, y, where= (x < t_critical), color='red', alpha=0.5)
        plt.axvline(t_stat, color='blue', linestyle='--', label=f't-statistic: {t_stat:.2f}')
        plt.axvline(t_critical, color='green', linestyle='--', label=f'Critical value: {t_critical:.2f}')
    elif tail == 'right':
        t_critical = stats.t.ppf(1 - alpha, df)
        plt.fill_between(x, y, where= (x > t_critical), color='red', alpha=0.5)
        plt.axvline(t_stat, color='blue', linestyle='--', label=f't-statistic: {t_stat:.2f}')
        plt.axvline(t_critical, color='green', linestyle='--', label=f'Critical value: {t_critical:.2f}')
    
    plt.legend()
    plt.title(f'T-distribution with df={df}')
    plt.show()

# Problem 1
plot_t_test(-0.286, 13, 0.05, 'two')

# Problem 2
plot_t_test(-1.646, 13, 0.01, 'left')

# Problem 3
plot_t_test(1.075, 13, 0.05, 'right')
