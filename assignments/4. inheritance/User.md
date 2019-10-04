# Inheritance

User
  -properties
    -name
    -score
  -methods
    -increaseScroe: returns score increased by 1
    -decreaseScore: returna score decreased by 1

PaidUser
  -properties
    -name
    -score
    -balance
  -methods
    -increaseScroe: returns score increased by 1
    -decreaseScore: returna score decreased by 1
    -increaseBalance: returna balance decreased by 1

Using Inheritance convert the above into following patterns.

1. Prototypal Pattern
2. Pseudoclassical Pattern
3. Classes

//1.Prototypal Pattern
const userMethods = {
  incrementScore : function() {
    this.score = this.score + 1;
    return this.score;
  },
  decrementScore : function() {
    this.score = this.score - 1;
    return this.score;
  }
};

function createuser(name, score) {
  var obj = Object.create(userMethods);
  obj.name = name;
  obj.score = score;
}

const paidUsersMethod = {
  incrementBalance : function() {
    this.balance = this.balance + 1;
    return this.balance;
  },
}

Object.setPrototypeOf(paidUsersMethod, userMethods);

function createPaidUser(name, score, balance) {
  var obj = createUser(name, score);
  Object.setPrototypeOf(obj, paidUsersMethod);
  obj.balance = balance;
  return obj;
}

//2. Pseudoclassical Pattern
const userMethods = {
    incrementScore : function(){
        this.score++;
        return this.score;
    },
    decrementScore : function(){
        this.score--;
        return this.score;
    }
};
function createUser (name, score) {
    this.name = name;  
    this.score = score;
}
createUser.prototype = userMethods;

function createPaidUser (name, score, balance) {
     createUser.call(this, name, score);
     this.balance = balance;
}
createUser.prototype.increamentBalance = function(){
    return this.balance++;
}
Object.setPrototypeOf(createPaidUser.prototype, createUser.prototype)

//3. Classes
class User {
    constructor(name, score){
        this.name = name;
        this.score = score;
    }
    incrementScore () {
        return this.score++;
    }
    decrementScore () {
        return this.score--;
    }
}
class PaidUser extends User {
    constructor(name, score, balance){
        super(name, score);
        this.balance = balance;
    }
    incrementBalance (){
        return this.balance++;
    }
}