# E-comerce


from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# Simulação de produtos (normalmente viria de um banco de dados)
products = [
    {'id': 1, 'name': 'Camiseta', 'price': 50},
    {'id': 2, 'name': 'Calça Jeans', 'price': 120},
    {'id': 3, 'name': 'Tênis', 'price': 250}
]

cart = []

@app.route('/')
def index():
    return render_template('index.html', products=products, cart=cart, total=sum(item['price'] for item in cart))

@app.route('/add_to_cart/<int:product_id>')
def add_to_cart(product_id):
    product = next((p for p in products if p['id'] == product_id), None)
    if product:
        cart.append(product)
    return redirect(url_for('index'))

@app.route('/clear_cart')
def clear_cart():
    cart.clear()
    return redirect(url_for('index'))

if __name__ == '__main__':
    app.run(debug=True)

"""
Estrutura de Pastas:
.
├── app.py
├── templates
│   └── index.html
├── static
│   └── style.css
└── README.md
"""

# Conteúdo do arquivo index.html (templates/index.html)
# ------------------------------------
# <!DOCTYPE html>
# <html lang="pt-br">
# <head>
#     <meta charset="UTF-8">
#     <meta name="viewport" content="width=device-width, initial-scale=1.0">
#     <link rel="stylesheet" href="/static/style.css">
#     <title>Mini E-commerce</title>
# </head>
# <body>
#     <h1>🛒 Mini E-commerce</h1>
#     <h2>Produtos:</h2>
#     <ul>
#         {% for product in products %}
#         <li>
#             {{ product.name }} - R$ {{ product.price }}
#             <a href="/add_to_cart/{{ product.id }}">[Adicionar ao Carrinho]</a>
#         </li>
#         {% endfor %}
#     </ul>
#     <h2>Carrinho:</h2>
#     <ul>
#         {% for item in cart %}
#         <li>{{ item.name }} - R$ {{ item.price }}</li>
#         {% endfor %}
#     </ul>
#     <p>Total: R$ {{ total }}</p>
#     <a href="/clear_cart">[Esvaziar Carrinho]</a>
# </body>
# </html>

# Conteúdo do arquivo style.css (static/style.css)
# ------------------------------------
# body {
#     font-family: 'Arial', sans-serif;
#     padding: 20px;
#     background-color: #f3f3f3;
# }
# h1 {
#     color: #333;
# }
# a {
#     color: #007BFF;
#     text-decoration: none;
#     margin-left: 10px;
# }
