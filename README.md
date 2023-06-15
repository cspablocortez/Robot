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

The `move` method simulates the movement of the robot delivering parcels. It takes one parameter: `destination` and its current location is `this.place`. It checks whether there's a valid road connection between its location and the destination. If there is not, it returns its current state. If there is a valid connection, on the other hand, it creates a new array of parcels using the `map()` function. For each parcel `p` in the current state's array, it checks whether the parcel's place (current location) matches the robot's place (current location). If they do match, it creates a new parcel object with the same address as the orginal parcel but with the place set to the destination. If they don't match, it returns the parcel as it is. 

After mapping the parcels, it filters the parcels to remove those that already reached their destination. It checks whether the `place` property is not equal to the `address` property for each parcel and filters out those that match. This ensures that only the parcels that still need to be delivered in the array.

At the end, the class returns a new `VillageState` instance with the `destination` as the new `place` and the updates `parcels` array. 