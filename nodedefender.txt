//Zumba Fitness Node Defender - Ultimate Developer Event 2013
//Collaboration included Winston Chen and Huy Le

// Available variables:
// _ - Access to underscore
// roundInfo - API for retrieving information from the server
// commander - API for sending commands to the server

//Declaration of the enemy that we will target and the attack modes of choice
var enemy, attackModes;

//Find the first enemy based on the following conditionals
for(var i = 0; i < roundInfo.getMobs().length; i++){
    if(roundInfo.getMobs()[i].type == "bruiser" || roundInfo.getMobs()[i].type == "trooper" && roundInfo.getMobs()[i].position === 0){
        enemy = roundInfo.getMobs()[i];
        break;
    }else if(roundInfo.getMobs()[i].type == "flyer" && roundInfo.getMobs()[i].position >= 4){
        enemy = roundInfo.getMobs()[i];
        break;
    }else if (roundInfo.getMobs()[i].type == "swarmer"){
        enemy = roundInfo.getMobs()[i];
        break;
    }else{
        enemy = roundInfo.getMobs()[i];
    }
}

//if the number of enemies is 5 or more, then target an enemy in that row
for(var i = 0; i < roundInfo.getMobs().length; i++){
    var count = 0;
        for(var j = 0; j < roundInfo.getMobs().length; j++){
            if(roundInfo.getMobs()[i].position == roundInfo.getMobs()[j].position){
                count++;
            }
            if(count >= 5){
                enemy = roundInfo.getMobs()[i];
                break;
            }
        }
}

//if the number of enemies is 3 or more, and they are in position 0, target an enemy in that row
for(var i = 0; i < roundInfo.getMobs().length; i++){
    var count = 0;
        for(var j = 0; j < roundInfo.getMobs().length; j++){
            if(roundInfo.getMobs()[i].position == roundInfo.getMobs()[j].position){
                count++;
            }
            if(count >= 3 && roundInfo.getMobs()[i].position === 0){
                enemy = roundInfo.getMobs()[i];
                break;
            }
        }
}

//third biggest priority
//if the flyers are at position 4 or more, then target the flyers
for(var i = 0; i < roundInfo.getMobs().length; i++){
    if(roundInfo.getMobs()[i].type == "flyer" && roundInfo.getMobs()[i].position >= 4){
        enemy = roundInfo.getMobs()[i];
        break;
    }
}

//second biggest priority
//if the count of enemies is 5 or more in any row, target an enemy in that row to avoid the accumulative damage
for(var i = 0; i < roundInfo.getMobs().length; i++){
    var count = 0;
        for(var j = 0; j < roundInfo.getMobs().length; j++){
            if(roundInfo.getMobs()[i].position == roundInfo.getMobs()[j].position && roundInfo.getMobs()[i].type == "cluster" && roundInfo.getMobs()[j].type == "cluster"){
                count++;
            }
            if(count >= 5){
                enemy = roundInfo.getMobs()[i];
                break;
            }
        }
}

//biggest priority
//if the bruisers or troopers get to position 0 or 1, target that bruiser or trooper
for(var i = 0; i < roundInfo.getMobs().length; i++){
    if((roundInfo.getMobs()[i].type == "bruiser" || roundInfo.getMobs()[i].type == "trooper") && (roundInfo.getMobs()[i].position === 0 || roundInfo.getMobs()[i].position == 1)){
        enemy = roundInfo.getMobs()[i];
        break;
    }
}

//declaration of enemy information
var id = enemy.id;
var type = enemy.type;
var position = enemy.position;
var health = enemy.health;

//Target the enemy
commander.target(id);

//initial designated attack modes to target the specified enemy
if(type == ("grunt")){
    commander.attackMode('rapid');
}else if(type == ("swarmer")){
    commander.attackMode('collateral');
}else if(type == ("trooper")){
    commander.attackMode('power');
}else if(type == ("speed-demon")){
    commander.attackMode('rapid');
}else if(type == ("flyer")){
    commander.attackMode('ranged');
}else if(type == ("cluster")){
    commander.attackMode('collateral');
}else if(type == ("bruiser")){
    commander.attackMode('power');
}

//some general commands based on position
if(enemy.position < 2){
    commander.attackMode('power');
}else if(enemy.position > 4){
    commander.attackMode('ranged');
}else{
    commander.attackMode('rapid');
}

//specific commands based on enemy type and position to override the previous commands
//I don't like clusters coming together in the early rounds
//Eliminate them to get the wave bonus
if(enemy.type == "cluster"){
    commander.attackMode('collateral');
}

//if the count of enemies becomes 5 in any row, use collateral on them to try to get the
//wave bonus
if(roundInfo.getMobs().length >= 4){
    for(var i = 0; i < roundInfo.getMobs().length; i++){
        var count = 0;
            for(var j = 0; j < roundInfo.getMobs().length; j++){
                if(roundInfo.getMobs()[i].position == roundInfo.getMobs()[j].position){
                    count ++;
                }
                if(count >= 5){
                    commander.attackMode('collateral');
                    break;
                }
            }
    }
}

//if the bruisers come to close and there are less than 15 enemies, use power to destroy them
//bruisers and troopers do too much damage close to the player
//Eliminate them as soon as possible to survive longer rounds
if((enemy.type == "bruiser" || enemy.type == "trooper") && enemy.position === 0 && roundInfo.getMobs().length < 15){
    commander.attackMode('power');
}

//if the amount of enemies is greater than 20, follow the general strategy for survivability
//likelihood of clearing 21 enemies is unlikely, so follow the general strategy to survive
if(roundInfo.getMobs().length > 20){
    if(enemy.position < 2){
        commander.attackMode('power');
    }else if(enemy.position > 4){
        commander.attackMode('ranged');
    }else{
        commander.attackMode('rapid');
    }
}

//if the amount of enemies is greater than 27, follow a defensive strategy, survive as long as possible
if(roundInfo.getMobs().length > 27){
    commander.attackMode('defensive');
}
