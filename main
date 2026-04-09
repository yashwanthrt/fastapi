from fastapi import FastAPI, Query
from fastapi.responses import HTMLResponse

app = FastAPI()

# ---- DATA ----
customers = [
    {"id": 1, "name": "Ravi Kumar", "city": "Hyderabad"},
    {"id": 2, "name": "Anjali Sharma", "city": "Delhi"},
    {"id": 3, "name": "Rahul Reddy", "city": "Bangalore"},
    {"id": 4, "name": "Ramesh Gupta", "city": "Hyderabad"},
    {"id": 5, "name": "Sneha Verma", "city": "Mumbai"},
    {"id": 6, "name": "Ritika Singh", "city": "Hyderabad"},
    {"id": 7, "name": "Arjun Mehta", "city": "Delhi"},
]

vendors = [
    {"id": 101, "name": "ABC Electronics", "product": "Mobiles", "city": "Hyderabad"},
    {"id": 102, "name": "XYZ Laptops", "product": "Laptops", "city": "Bangalore"},
    {"id": 103, "name": "TechWorld", "product": "Accessories", "city": "Mumbai"},
    {"id": 104, "name": "Reddy Mobiles", "product": "Mobiles", "city": "Hyderabad"},
    {"id": 105, "name": "Digital Hub", "product": "Laptops", "city": "Delhi"},
]

# ---- HOME ----
@app.get("/", response_class=HTMLResponse)
def home():
    return """
    <html>
        <body style="font-family: Arial; text-align:center; margin-top:50px;">
            <h1>Dashboard</h1>
            <a href="/customers"><button>Customers</button></a>
            <a href="/vendors"><button>Vendors</button></a>
            <br><br>
            <p>Try filters:</p>
            <p>/customers?city=Hyderabad</p>
            <p>/customers?starts_with=R</p>
        </body>
    </html>
    """

# ---- FILTER FUNCTION ----
def filter_data(data, city=None, starts_with=None):
    result = data

    if city:
        result = [d for d in result if d["city"].lower() == city.lower()]

    if starts_with:
        result = [d for d in result if d["name"].lower().startswith(starts_with.lower())]

    return result

# ---- CUSTOMERS ----
@app.get("/customers", response_class=HTMLResponse)
def get_customers(city: str = Query(None), starts_with: str = Query(None)):
    filtered = filter_data(customers, city, starts_with)

    rows = "".join([
        f"<li>ID: {c['id']} | {c['name']} - {c['city']}</li>"
        for c in filtered
    ])

    return f"""
    <html>
        <body style="font-family: Arial; padding:20px;">
            <h2>Customers</h2>
            <ul>{rows}</ul>
            <a href="/">⬅ Back</a>
        </body>
    </html>
    """

# ---- VENDORS ----
@app.get("/vendors", response_class=HTMLResponse)
def get_vendors(city: str = Query(None), starts_with: str = Query(None)):
    filtered = filter_data(vendors, city, starts_with)

    rows = "".join([
        f"<li>ID: {v['id']} | {v['name']} - {v['product']} ({v['city']})</li>"
        for v in filtered
    ])

    return f"""
    <html>
        <body style="font-family: Arial; padding:20px;">
            <h2>Vendors</h2>
            <ul>{rows}</ul>
            <a href="/">⬅ Back</a>
        </body>
    </html>
    """
