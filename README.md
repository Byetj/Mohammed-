# Mohammed-
Clothing brand class Product:
    def __init__(self, name, category, price, quantity):
        self.name = name
        self.category = category
        self.price = price
        self.quantity = quantity
        
    def update_quantity(self, quantity):
        self.quantity += quantity
        
class Inventory:
    def __init__(self):
        self.products = []
        
    def add_product(self, product):
        self.products.append(product)
        
    def remove_product(self, product):
        self.products.remove(product)
        
    def find_product(self, name):
        for product in self.products:
            if product.name == name:
                return product
        return None
        
class Sales:
    def __init__(self):
        self.sales = []
        
    def add_sale(self, sale):
        self.sales.append(sale)
        
class Sale:
    def __init__(self, product, quantity):
        self.product = product
        self.quantity = quantity
        self.total_price = product.price * quantity
        
class ClothingLine:
    def __init__(self):
        self.inventory = Inventory()
        self.sales = Sales()
        
    def add_product(self, name, category, price, quantity):
        product = Product(name, category, price, quantity)
        self.inventory.add_product(product)
        
    def remove_product(self, name):
        product = self.inventory.find_product(name)
        if product:
            self.inventory.remove_product(product)
            
    def update_product_quantity(self, name, quantity):
        product = self.inventory.find_product(name)
        if product:
            product.update_quantity(quantity)
            
    def make_sale(self, name, quantity):
        product = self.inventory.find_product(name)
        if product and product.quantity >= quantity:
            sale = Sale(product, quantity)
            self.sales.add_sale(sale)
            product.update_quantity(-quantity)
            return sale
        return None
