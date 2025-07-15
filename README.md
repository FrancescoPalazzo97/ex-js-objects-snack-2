# 🍔 EX - Snack Oggetti

**📁 Repo:** ex-js-objects-snack-2

## 🏆 Code Question 1

```javascript
const hamburger = { name: "Cheese Burger", weight: 250 };
const secondBurger = hamburger;
secondBurger.name = 'Double Cheese Burger';
secondBurger.weight = 500;

console.log(hamburger.name); // ?
console.log(secondBurger.name ); // ?
```

* Senza lanciare il codice, riesci a prevedere cosa viene stampato in console?

In console verrà stampato 'Double Cheese Burger' per entrambi i console.log

* Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

È stato creato un oggetto

---

## 🏆 Code Question 2

```javascript
const hamburger = { 
    name: "Cheese Burger", 
    weight: 250,
    ingredients: ["Cheese", "Meat", "Bread", "Tomato"]
};

const secondBurger = {...hamburger};
secondBurger.ingredients[0] = "Salad";

console.log(hamburger.ingredients[0]); // ?
console.log(secondBurger.ingredients[0]); // ?
```

**P.S.:** Ricordati che gli Array, come gli oggetti, sono dei Reference Type (Tipi di Riferimento)!

* Senza lanciare il codice, riesci a prevedere cosa viene stampato in console?

In console verrà stampato "Salad" per entrambi i console.log

* Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

Sono stati creati 2 oggetti

---

## 🏆 Code Question 3

```javascript
const hamburger = { 
    name: "Cheese Burger", 
    weight: 250,
    maker: {
        name: "Anonymous Chef",
        restaurant: {
            name: "Hyur's Burgers",
            address: "Main Street, 123",
            isOpen: true,
        },
        age: 29
    }
};

const secondBurger = structuredClone(hamburger);
const thirdBurger = structuredClone(hamburger);
```

* Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

9 oggetti

---

## 🏆 Code Question 4

```javascript
const chef = {
    name: "Chef Hyur",
    age: 29,
    makeBurger: (num = 1) => {
        console.log(`Ecco ${num} hamburger per te!`);
    },
}

const restaurant = {
    name: "Hyur's Burgers",
    address: {
        street: 'Main Street',
        number: 123,
    },
    openingDate: new Date(2025, 3, 11),
    isOpen: false,
};
```

* Qual è il metodo migliore per clonare l'oggetto chef, e perché?

Il miglior modo di clonare chef è usando lo spread operator con il qualte posso clonare anche la funzione presente all'interno

* Qual è il metodo migliore per clonare l'oggetto restaurant, e perché?

Per restaurant il miglior modo è stucturedClone() che permette di clonare anche gli oggetti annidati e anche Date

## 🎯 Code Question 5 (Bonus)

```javascript
const hamburger = { 
    name: "Cheese Burger", 
    weight: 250,
    maker: {
        name: "Anonymous Chef",
        restaurant: {
            name: "Hyur's Burgers",
            address: "Main Street, 123",
            isOpen: true,
        },
        age: 29
    }
};

const newRestaurant = {...hamburger.maker.restaurant};
newRestaurant.name = "Hyur's II";
newRestaurant.address = "Second Street, 12";
const secondBurger = {...hamburger};
secondBurger.maker.restaurant = newRestaurant;
secondBurger.maker.name = "Chef Hyur";

console.log(hamburger.maker.name); // ?
console.log(secondBurger.maker.name); // ?
console.log(hamburger.maker.restaurant.name); // ?
console.log(secondBurger.maker.restaurant.name); // ?
```

* Senza lanciare il codice, riesci a prevedere cosa viene stampato in console?

1. "Chef Hyur" per il primo console.log
2. "Chef Hyur" anche per il secondo
3. "Hyur's II" per il terzo
4. "Hyur's II" anche per il quarto

* Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

5 oggetti in totale

## 🎯 Code Question 6 (Bonus)

```javascript
const chef = {
    name: "Chef Hyur",
    age: 29,
    makeBurger: (num = 1) => {
        console.log(`Ecco ${num} hamburger per te!`);
    },
    restaurant: {
        name: "Hyur's Burgers",
        welcomeClient: () => {
            console.log("Benvenuto!");
        },
        address: {
            street: 'Main Street',
            number: 123,
            showAddress: () => {
                console.log("Main Street 123");
            }
        },
        isOpen: true,
    }
}
```

* Qual è il metodo migliore per clonare l'oggetto chef, e perché?

Il modo migliore è il seguente:
```javascript
const chefCopy = {
    ...chef,
    restaurant: {
        chef.restaurant,
        address: {
            chef.restaurant.address
        }
    }
}
```


## 🎯 Snack (Bonus)

Crea una funzione che permette la copia profonda (deep copy) di un oggetto, che copia anche i suoi metodi (proprietà che contengono funzioni). Usa l'oggetto di Code Question 6 come test. 

⚠️ **Serve usare una funzione ricorsiva!** (fai un po' di ricerca).

Oggetto originale
```javascript
const chef = {
    name: "Chef Hyur",
    age: 29,
    makeBurger: (num = 1) => {
        console.log(`Ecco ${num} hamburger per te!`);
    },
    restaurant: {
        name: "Hyur's Burgers",
        welcomeClient: () => {
            console.log("Benvenuto!");
        },
        address: {
            street: 'Main Street',
            number: 123,
            showAddress: () => {
                console.log("Main Street 123");
            }
        },
        isOpen: true,
    }
}
```

Funzione per clonare:

```javascript
function deepCopy(obj) {
    if (typeof obj !== 'object'){
        return obj;
    }
    if(Array.isArray(obj)){
        return obj.map(value => deepCopy(value));
    }
    const copy = {};
    for(const key in obj) {
        const value = obj[key];
        copy[key] = deepCopy(value);
    }
    return copy;
}
```