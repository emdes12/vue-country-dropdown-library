# USING COUNTRY LIBRARY IN VUE

![country and state dropdown](https://static.skillshare.com/uploads/discussion/tmp/b8a9848c)
Hi!

In here, I explained how to used the country library in **vue.js**

The country list and the states list was split into different file and can be located in [list of countries](/src/assets/country.js) and  [list of states](/src/assets/stateArr.js)
**NB** the list are in form of **Objects in Array**

## Importing to your Vue 

After knowing our list location, the next thing is to import, in your script, immediately after the script opening tag `<script>` import the files. eg

    import  country  from  "@/assets/country.js";
    import  states  from  "@/assets/stateArr.js";

**NB** we don't use ~~/../src/assets/country.js~~ or ~~src/assets/stateArr.js~~ and we use `@` instead which refer the path upward to a parent directory that contain `assets/` folder.
 

## Storing the imported data

importing the files doesn't mean having access to it, we still have to store the data

    export  default {
      data() {
        return {
          country:  country,
          states:  states,
        };
      },
    };

## Display the country list in it Selecting field

Now let run fast, in your template tag add this;

    <template>
      <select name="country">
          <option v-for="(list, index) in  country" :key="index" value="list.name"> {{ list.name }} </option>
      </select>
    </template>
Where;

 - **list** is represent each Object in the Array
 - and **index** is the indexOf the object

We then loop through the array using **For In Loop** `for ____ in _____` *JS* but which is the same as `v-for="____ in  ____"` in *VUE.js*

## Displaying State in it Selecting field
Here we have works to do. Hey, let's **GO**

### Getting selected country id index
We have to first get the country selected and indexOf the value.  
**Now** lets go on research think of a way you of doing doing this.
**HINT** the country and it state as the same index.

- 1
- 2
- 3
- 4
- 5
Wait! Wait!! Wait!!!

I said wait **HOLD ON**

I can see you are waiting for me to drop it. No P, here is it.
#### Make and eventListener to handle that
##### Add a function to handler that
In your `<script>` tag add a methods for functions input then define your function.

    <script>
      import  headers  from  "@/components/headers.vue";
      import  country  from  "@/assets/country.js";
      import  states  from  "@/assets/stateArr.js";
    
      export  default {
        data() {
          return {
            country:  country,
            states:  states,
          };
        },
        methods: {
          atChange(event) {
            let  countryIndex = 0;
            for (let  i = 0; i < this.country.length; i++) {
              if (this.country[i].name === event.target.value) {
                countryIndex = i + 1;
             }
          }
          this.populatedState = this.states[countryIndex].name.split("|");
        },
      },
    };
    </script>

No ES6 function is used. So I believe you should understand. Thanks for that.


##### Call your function in the Selecting tag for Country
Within you templates tag, modify your input to have an onChange eventListener that call a function
 
    <select name="country" @change="atChange($event)">
      <option v-for="(list, index) in  country" :key="index" :value="list.name"> {{ list.name }} </option>
    </select>
 
 #### Passing the output to selecting tag state
 Now we created a function which get he value of select tag for country then find the indexOf it the in the country Array and pass the index as index in the state Array, then store the values of the state that has the same array.indexOf() with the selected country to a new variable as array what left for us is to pass. What next!

##### We have  to create our state selecting tag
add the below code within your template tag.

    <select name="state" >
          <option value=""> Select a state </option>
    </select>
after your country selecting tag.
##### Let's show the state within a selected country
Here, we are doing the same thing to display the states (i.e **looping through**)  

<template>
  

    <select name="country">
          <option v-for="(list, index) in  country" :key="index" value="list.name"> {{ list.name }} </option>
      </select>
      
      <select name="country" @change="atChange($event)">
          <option v-for="(state, index) in  populatedState" :key="index" value="state.name"> {{ state.name }} </option>
      </select>
    </template>

Thanks for reading and using this library.

Thanks to [@Top_Universe](https://topuniverse/org) for this opportunity.
