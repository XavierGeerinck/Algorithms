# Evolutionary Computation
```
/**
 * @author: Xavier Geerinck
 * @title: Heuristics - Evolutionary Computation
 * @subtitle: 
 * @method:
 * 1. Create a population
 * 2. Check the fitness of the individuals of the population
 * 3. As long as termination condition not met, continue
 *     i. Recombine: take 2 parents and combine them
 *     ii. Mutate: For the new child, change some properties based on a mutation parameter
 *     iii. Generational Replacement: Check the fitness level of the mutated child, and add it if it is better
  */
 
class Gene {
    constructor(code) {
        if (code) {
            this.code = code;
        }

        this.cost = 9999;
    }

    random(length) {
        while (length--) {
            this.code += String.fromCharCode(Math.floor(Math.random() * 255));
        }
    }

    mutate(chance) {
        if (Math.random() > chance) {
            return;
        }

        var index = Math.floor(Math.random() * this.code.length);
        var upOrDown = Math.random() <= 0.5 ? -1 : 1;
        var newChar = String.fromCharCode(this.code.charCodeAt(index) + upOrDown);
        var newString = '';
        for (var i = 0; i < this.code.length; i++) {
            if (i == index) newString += newChar;
            else newString += this.code[i];
        }

        this.code = newString;
    }

    mate(gene) {
        var pivot = Math.round(this.code.length / 2) - 1;

        var child1 = this.code.substr(0, pivot) + gene.code.substr(pivot);
        var child2 = gene.code.substr(0, pivot) + this.code.substr(pivot);

        return [new Gene(child1), new Gene(child2)];
    }

    calcCost(compareTo) {
        var total = 0;
        for (var i = 0; i < this.code.length; i++) {
            total += (this.code.charCodeAt(i) - compareTo.charCodeAt(i)) * (this.code.charCodeAt(i) - compareTo.charCodeAt(i));
        }
        this.cost = total;
    }
}

class Population {
    constructor(goal, size) {
        this.members = [];
        this.goal = goal;
        this.generationNumber = 0;
        while (size--) {
            var gene = new Gene();
            gene.random(this.goal.length);
            this.members.push(gene);
        }
    }

    display() {
        document.body.innerHTML = '';
        document.body.innerHTML += ("<h2>Generation: " + this.generationNumber + "</h2>");
        document.body.innerHTML += ("<ul>");
        for (var i = 0; i < this.members.length; i++) {
            document.body.innerHTML += ("<li>" + this.members[i].code + " (" + this.members[i].cost + ")");
        }
        document.body.innerHTML += ("</ul>");
    }

    sort() {
        this.members.sort(function(a, b) {
            return a.cost - b.cost;
        });
    }

    generation() {
        for (var i = 0; i < this.members.length; i++) {
            this.members[i].calcCost(this.goal);
        }

        this.sort();
        this.display();
        var children = this.members[0].mate(this.members[1]);
        this.members.splice(this.members.length - 2, 2, children[0], children[1]);

        for (var i = 0; i < this.members.length; i++) {
            this.members[i].mutate(0.5);
            this.members[i].calcCost(this.goal);
            if (this.members[i].code == this.goal) {
                this.sort();
                this.display();
                return true;
            }
        }
        this.generationNumber++;
        var scope = this;
        setTimeout(function() {
            scope.generation();
        }, 20);
    }
}

var population = new Population("Hello, world!", 20);
population.generation();
```
