# Robot


 From Eloquent JavaScript [Chapter 7](https://eloquentjavascript.net/07_robot.html): 
 
 > Our project in this chapter is to build an automaton, a little program that performs a task in a virtual world. Our automaton will be a mail-delivery robot picking up and dropping off parcels.

 The village of Meadowfield.

 ![Meadowfield](https://eloquentjavascript.net/img/village2x.png)

 ## Class VillageState

 ```javascript
class VillageState {
    constructor(place, parcels) {
        this.place = place;
        this.parcels = parcels;
    }

    move(destination) {
        if(!roadGraph[this.place].includes(destination)) {
            return this;
        } else {
            let parcels = this.parcels.map(p => {
                if (p.place != this.place) return p;
                return {place: destination, address: p.address};
            }).filter(p => p.place != p.address);
            return new VillageState(destination, parcels);
        }
    }
}
 ```

The class `VillageState` represents the Meadowfield town's state.

```javascript
class VillageState {
    constructor(place, parcels) {
        this.place = place;
        this.parcels = parcels;
    }
}
```

The `constructor` method initializes a new instance of the `VillageState` class. It takes two parameters: `place` and `parcels`.

`place`: specifies the robot's current location.

`parcels`: an array of objects representing the parcels.

The `move` method simulates the movement of the robot delivering parcels. It takes one parameter: `destination` and its current location is `this.place`. It checks wheter there's a valid road connection between its location and the destination. If there is not, it returns its current state.





