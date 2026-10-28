Sample Business: 
```yaml
id: business_0006

name: Holy Frijoles & Amigos

description: A playful cantina where bold flavors and inventive twists meet tradition.

  Enjoy a delicious fusion of classic and contemporary Mexican and Tex-Mex bites,

  crafted for both the curious and the comfort-seekers.

rating: 1.0

progenitor_customer: customer_0002

menu_features:

  Cinnamon Dulce Nachos: 9.89

  Three-Cheese Empanadas: 10.43

  Tamarind Agua Fresca: 4.32

  Carnitas Salsa Verde Tacos: 13.62

  Cactus and Black Bean Tacos: 12.02

  Ancho-Coffee Rubbed Steak: 24.77

  Matcha Horchata Freeze: 5.29

  Chipotle Chicken Quesadilla: 8.22

  Fresh Guacamole Platter: 8.56

  Green Chili Chicken Soup: 9.16

  Sunrise Breakfast Burrito: 9.93

  Spiced Avocado Toast: 8.01

  Pineapple Habanero Salsa: 6.85

  Agave Lime Glazed Wings: 11.04

  Tex-Mex Breakfast Skillet: 11.66

  Roasted Vegetable Tacos: 12.32

  Smoky Chipotle Beef Skewers: 14.26

amenity_features:

  Children's Menu: false

  Large Groups: true

  Live Music: false

  Free Wifi: true

  Wheelchair Accessible: false

  Onsite Parking: true

  Happy Hour: false

  Private Dining: false

  Outdoor Seating: false

  Takes Reservations: true

min_price_factor: 0.65
```

```yaml
id: customer_0002

name: Chloe Zhang

request: 'Could you please assist me in finding a business that offers the following

  menu items: a ''Fresh Guacamole Platter'' (1), a ''Tex-Mex Breakfast Skillet'' (1),

  and a ''Green Chili Chicken Soup'' (1), and that also has the amenity of being ''Wheelchair

  Accessible''? It is important that all these requirements are met as I intend to

  place an order. Thank you for your assistance.'

menu_features:

  Fresh Guacamole Platter: 8.49

  Tex-Mex Breakfast Skillet: 11.49

  Green Chili Chicken Soup: 8.5

amenity_features:

- Wheelchair Accessible
```
- Current lexical search is based off of a simple n-gram similarity search. 
- Database rows essentially store an agent description, which captures the descriptions of the business, plus embedding for a formatted version of the business metadata.
``` business_0003 | {"id": "business_0003", "name": "Verde & Ember", "type": "business", "rating": 1.0, "description": "A vibrant spot for modern Mexican and Tex-Mex flavors, Verde & Ember brings fresh ingredients and creative twists to classic favorites. Enjoy bold, colorful dishes and house-made s
alsas in a lively, welcoming atmosphere.", "menu_features": {"Blackened Fish Tacos": 13.87, "Spicy Beef Empanadas": 11.06, "Tomatillo Verde Salsa": 4.5, "Spicy Black Bean Burger": 13.99, "Hatch Green Chile Burger": 9.9, "Savory Pumpkin Empanadas": 9.31, "Blue Corn Chicken Tamales": 9.87, "Verde C
hicken Chimichanga": 17.48, "Black Bean Avocado Burrito": 10.26, "Honey Lime Chicken Fajitas": 14.27, "Fiery Chipotle Chicken Salad": 11.41, "Spicy Verde Chicken Tostadas": 9.43, "Pineapple Jalapeno Agua Fresca": 5.03}, "amenity_features": {"Free Wifi": false, "Happy Hour": false, "Live Music": t
rue, "Large Groups": false, "Onsite Parking": false, "Private Dining": false, "Children's Menu": false, "Outdoor Seating": false, "Takes Reservations": false, "Wheelchair Accessible": true}, "min_price_factor": 0.84, "progenitor_customer": "customer_0001"}
```
- min_price_factor and numeric value in menu_features are not actually used at all in the experiment, could be an avenue worth exploring.
- **https://a2a-protocol.org/latest/tutorials/python/3-agent-skills-and-card/** Important link for doing a2a using python sdk.
- Idea: Have once central marketplace agent: 
	- Search tool: Connect it to lexical / embedding search
	- Message tool: Negotiate about order
	- Proposal can be done in an update to Task? It's weird that proposal is initiated by business and not customer.
- A2A RequestContext object: 
	```python
	class RequestContext:
    # The incoming message from the client
    message: Message

    # Existing task, if this request is continuing one
    current_task: Task | None

    # Unique conversation/context id
    context_id: str

    # Authentication / session information
    metadata: dict

    # Convenience helper
    def get_user_input() -> str: ...
	```
- All available actions are under the platform/server/routes folder, if we want to change something, we can change it there.
- 
