 import numpy as np

# Визначимо функцію, яка відповідає рівнянню 6x^4 + 4x^3 - x^2 - x - 10 = 0
def f(x):
    return 6 * pow(x, 4) + 4 * pow(x, 3) - pow(x, 2) - x - 10

# Метод ділення пополам
def rec(a, b, eps):
    while (abs(a - b) > eps):
        if (f(a) * f((a + b) / 2) < 0):
            b = (a + b) / 2
        else:
            a = (a + b) / 2
        x = (a + b) / 2
    print('x= ', round(x, 5), '  - Метод ділення пополам')

# Метод хорд
def hord(a, b, eps):
    if (f(a) * ((f(a + eps) - 2 * f(a) + f(a - eps)) / (eps ** 2)) > 0):
        x0, xi = a, b
    else:
        x0, xi = b, a
    xi_1 = xi - (xi - x0) * f(xi) / (f(xi) - f(x0))
    while (abs(xi_1 - xi) > eps):
        xi = xi_1
        xi_1 = xi - (xi - x0) * f(xi) / (f(xi) - f(x0))
    print('x= ', round(xi_1, 5), '  - Метод хорд')

# Заданий епсілон
eps = 0.0001

# Знайдемо корені полінома за допомогою numpy.roots
roots = np.roots([6, 4, -1, -1, -10])

# Застосовуємо методи для знайдених коренів
for root in roots:
    if np.isreal(root):
        root = np.real(root)
        print("Root:", round(root, 5))
        rec(root - 0.1, root + 0.1, eps)
        hord(root - 0.1, root + 0.1, eps)
