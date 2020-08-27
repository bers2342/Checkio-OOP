# Taken from mission Straight Fight

# Taken from mission The Healers

# Taken from mission The Lancers

# Taken from mission The Vampires

# Taken from mission The Defenders

# Taken from mission Army Battles

# Taken from mission The Warriors

class Warrior(object):
    def __init__(self):
        self.health = 50
        self.max_life = self.health
        self.attack = 5
        self.lance_dmg = 0
        self.defense = 0
        self.vampirism = 0
        self.heal_power = 0
        self.is_alive = True
    
    def hit(self, enemy_unit):
        enemy_unit.health -= max(self.attack - enemy_unit.defense, 0)
        self.health += int(float(self.vampirism)/100*max(self.attack - enemy_unit.defense, 0))
        
    def lance_hit(self, enemy_unit):
        enemy_unit.health -= max(self.lance_dmg - enemy_unit.defense, 0)
        
    def heal(self, allied_unit):
        allied_unit.health = min(allied_unit.health + self.heal_power, allied_unit.max_life)
 
    def equip_weapon(self, weapon_name):
        self.health += weapon_name.health
        self.attack += weapon_name.attack
        
        if self.heal_power>0:
            self.heal_power += weapon_name.heal_power
        
        if self.vampirism>0:
            self.vampirism += weapon_name.vampirism
            
        if self.defense>0:
            self.defense += weapon_name.defense
     
class Knight(Warrior):
    def __init__(self):
        Warrior.__init__(self)
        self.attack = 7
        
class Defender(Warrior):
    def __init__(self):
        Warrior.__init__(self)
        self.health = 60
        self.max_life = self.health
        self.attack = 3
        self.defense = 2
        
class Vampire(Warrior):
    def __init__(self):
        Warrior.__init__(self)
        self.health = 40
        self.max_life = self.health
        self.attack = 4 
        self.vampirism = 50


class Lancer(Warrior):
    def __init__(self):
        Warrior.__init__(self)
        self.attack = 6
        self.lance_dmg = int(0.5*self.attack)
        
class Healer(Warrior):
    def __init__(self):
        Warrior.__init__(self)
        self.health = 60
        self.max_life = self.health
        self.attack = 0
        self.heal_power = 2

class Weapon(object):
    def __init__(self, health, attack, defense, vampirism, heal_power):
        self.health = health
        self.attack = attack
        self.defense = defense
        self.vampirism = vampirism
        self.heal_power = heal_power

class Sword(Weapon):
    def __init__(self):
        Weapon.__init__(self, 5, 2, 0, 0, 0)

class Shield(Weapon):
    def __init__(self):
        Weapon.__init__(self, 20, -1, 2, 0, 0)

class GreatAxe(Weapon):
    def __init__(self):
        Weapon.__init__(self, -15, 5, -2, 10, 0)

class Katana(Weapon):
    def __init__(self):
        Weapon.__init__(self, -20, 6, -5, 50, 0)
        
class MagicWand(Weapon):
    def __init__(self):
        Weapon.__init__(self, 30, 3, 0, 0, 3)


class Commentator(object):
    def __init__(self, army_1, army_2):
        self.army_1 = army_1
        self.army_2 = army_2
    
    def comment(self):
        print('health of army 1 : '+str([self.army_1[i].health for i in range(len(self.army_1))])+'\n'+
        'health of army 2 : '+str([self.army_2[i].health for i in range(len(self.army_2))])+'\n')


def fight(unit_1, unit_2):
    while unit_1.health>0 or unit_2.health>0:
        unit_1.hit(unit_2)
        if unit_2.health<=0:
            unit_2.is_alive = False
            return True
        unit_2.hit(unit_1)
        if unit_1.health<=0:
            unit_1.is_alive = False
            return False


class Army(object):
    def __init__(self):
        self.units = []
    
    def add_units(self, unit, number):
        for i in range(number):
            self.units.append(unit())
            
class Battle(object):
    def fight(self, army_1, army_2):
        commentator = Commentator(army_1.units, army_2.units)
        while army_1.units != [] or army_2.units != []:
            # Army 1 Phase
            army_1.units[0].hit(army_2.units[0])
            if len(army_2.units)>1:
                army_1.units[0].lance_hit(army_2.units[1]) 
            if len(army_1.units)>1:
                army_1.units[1].heal(army_1.units[0])
            for unit in army_2.units:
                if unit!=army_2.units[0] and unit.health<=0:
                    army_2.units.remove(unit)
            if army_2.units[0].health<=0:
                army_2.units[0].is_alive = False
                army_2.units.remove(army_2.units[0])
                if army_2.units == []:
                    return True
                army_1.units[0].hit(army_2.units[0])
                if len(army_2.units)>1:
                    army_1.units[0].lance_hit(army_2.units[1]) 
                if len(army_1.units)>1:
                    army_1.units[1].heal(army_1.units[0])
            # Army 2 Phase
            army_2.units[0].hit(army_1.units[0])
            if len(army_1.units)>1:
                army_2.units[0].lance_hit(army_1.units[1]) 
            if len(army_2.units)>1:
                army_2.units[1].heal(army_2.units[0])
            for unit in army_1.units:
                if unit!=army_1.units[0] and unit.health<=0:
                    army_1.units.remove(unit)
            if army_1.units[0].health<=0:
                army_1.units[0].is_alive = False
                army_1.units.remove(army_1.units[0])
                if army_1.units == []:
                    return False
            #commentator.comment()
            
    def straight_fight(self, army_1, army_2):
        while army_1.units != [] and army_2.units != []:
            for i in range(min(len(army_1.units), len(army_2.units))):
                if fight(army_1.units[i], army_2.units[i]):
                    army_2.units[i] = 0
                else:
                    army_1.units[i] = 0
            while 0 in army_1.units:
                army_1.units.remove(0)
            while 0 in army_2.units:
                army_2.units.remove(0)
        return bool(army_1.units)



if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing

    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False

    print("Coding complete? Let's try tests!")

if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
    #fight tests
    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False

    #battle tests
    my_army = Army()
    my_army.add_units(Knight, 3)
    
    enemy_army = Army()
    enemy_army.add_units(Warrior, 3)

    army_3 = Army()
    army_3.add_units(Warrior, 20)
    army_3.add_units(Knight, 5)
    
    army_4 = Army()
    army_4.add_units(Warrior, 30)

    battle = Battle()

    assert battle.fight(my_army, enemy_army) == True
    assert battle.fight(army_3, army_4) == False
    print("Coding complete? Let's try tests!")


if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
    #fight tests
    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()
    bob = Defender()
    mike = Knight()
    rog = Warrior()
    lancelot = Defender()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False
    assert fight(bob, mike) == False
    assert fight(lancelot, rog) == True

    #battle tests
    my_army = Army()
    my_army.add_units(Defender, 1)
    
    enemy_army = Army()
    enemy_army.add_units(Warrior, 2)

    army_3 = Army()
    army_3.add_units(Warrior, 1)
    army_3.add_units(Defender, 1)

    army_4 = Army()
    army_4.add_units(Warrior, 2)

    battle = Battle()

    assert battle.fight(my_army, enemy_army) == False
    assert battle.fight(army_3, army_4) == True
    print("Coding complete? Let's try tests!")


if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
    #fight tests
    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()
    bob = Defender()
    mike = Knight()
    rog = Warrior()
    lancelot = Defender()
    eric = Vampire()
    adam = Vampire()
    richard = Defender()
    ogre = Warrior()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False
    assert fight(bob, mike) == False
    assert fight(lancelot, rog) == True
    assert fight(eric, richard) == False
    assert fight(ogre, adam) == True

    #battle tests
    my_army = Army()
    my_army.add_units(Defender, 2)
    my_army.add_units(Vampire, 2)
    my_army.add_units(Warrior, 1)
    
    enemy_army = Army()
    enemy_army.add_units(Warrior, 2)
    enemy_army.add_units(Defender, 2)
    enemy_army.add_units(Vampire, 3)

    army_3 = Army()
    army_3.add_units(Warrior, 1)
    army_3.add_units(Defender, 4)

    army_4 = Army()
    army_4.add_units(Vampire, 3)
    army_4.add_units(Warrior, 2)

    battle = Battle()

    assert battle.fight(my_army, enemy_army) == False
    assert battle.fight(army_3, army_4) == True
    print("Coding complete? Let's try tests!")

if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
    #fight tests
    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()
    bob = Defender()
    mike = Knight()
    rog = Warrior()
    lancelot = Defender()
    eric = Vampire()
    adam = Vampire()
    richard = Defender()
    ogre = Warrior()
    freelancer = Lancer()
    vampire = Vampire()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False
    assert fight(bob, mike) == False
    assert fight(lancelot, rog) == True
    assert fight(eric, richard) == False
    assert fight(ogre, adam) == True
    assert fight(freelancer, vampire) == True
    assert freelancer.is_alive == True

    #battle tests
    my_army = Army()
    my_army.add_units(Defender, 2)
    my_army.add_units(Vampire, 2)
    my_army.add_units(Lancer, 4)
    my_army.add_units(Warrior, 1)
    
    enemy_army = Army()
    enemy_army.add_units(Warrior, 2)
    enemy_army.add_units(Lancer, 2)
    enemy_army.add_units(Defender, 2)
    enemy_army.add_units(Vampire, 3)

    army_3 = Army()
    army_3.add_units(Warrior, 1)
    army_3.add_units(Lancer, 1)
    army_3.add_units(Defender, 2)

    army_4 = Army()
    army_4.add_units(Vampire, 3)
    army_4.add_units(Warrior, 1)
    army_4.add_units(Lancer, 2)

    battle = Battle()

    assert battle.fight(my_army, enemy_army) == True
    assert battle.fight(army_3, army_4) == False
    print("Coding complete? Let's try tests!")

if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
    #fight tests
    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()
    bob = Defender()
    mike = Knight()
    rog = Warrior()
    lancelot = Defender()
    eric = Vampire()
    adam = Vampire()
    richard = Defender()
    ogre = Warrior()
    freelancer = Lancer()
    vampire = Vampire()
    priest = Healer()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False
    assert fight(bob, mike) == False
    assert fight(lancelot, rog) == True
    assert fight(eric, richard) == False
    assert fight(ogre, adam) == True
    assert fight(freelancer, vampire) == True
    assert freelancer.is_alive == True
    assert freelancer.health == 14    
    priest.heal(freelancer)
    assert freelancer.health == 16

    #battle tests
    my_army = Army()
    my_army.add_units(Defender, 2)
    my_army.add_units(Healer, 1)
    my_army.add_units(Vampire, 2)
    my_army.add_units(Lancer, 2)
    my_army.add_units(Healer, 1)
    my_army.add_units(Warrior, 1)
    
    enemy_army = Army()
    enemy_army.add_units(Warrior, 2)
    enemy_army.add_units(Lancer, 4)
    enemy_army.add_units(Healer, 1)
    enemy_army.add_units(Defender, 2)
    enemy_army.add_units(Vampire, 3)
    enemy_army.add_units(Healer, 1)

    army_3 = Army()
    army_3.add_units(Warrior, 1)
    army_3.add_units(Lancer, 1)
    army_3.add_units(Healer, 1)
    army_3.add_units(Defender, 2)

    army_4 = Army()
    army_4.add_units(Vampire, 3)
    army_4.add_units(Warrior, 1)
    army_4.add_units(Healer, 1)
    army_4.add_units(Lancer, 2)

    battle = Battle()

    assert battle.fight(army_3, army_4) == True
    assert battle.fight(my_army, enemy_army) == False
    print("Coding complete? Let's try tests!")


if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
    #fight tests
    chuck = Warrior()
    bruce = Warrior()
    carl = Knight()
    dave = Warrior()
    mark = Warrior()
    bob = Defender()
    mike = Knight()
    rog = Warrior()
    lancelot = Defender()
    eric = Vampire()
    adam = Vampire()
    richard = Defender()
    ogre = Warrior()
    freelancer = Lancer()
    vampire = Vampire()
    priest = Healer()

    assert fight(chuck, bruce) == True
    assert fight(dave, carl) == False
    assert chuck.is_alive == True
    assert bruce.is_alive == False
    assert carl.is_alive == True
    assert dave.is_alive == False
    assert fight(carl, mark) == False
    assert carl.is_alive == False
    assert fight(bob, mike) == False
    assert fight(lancelot, rog) == True
    assert fight(eric, richard) == False
    assert fight(ogre, adam) == True
    assert fight(freelancer, vampire) == True
    assert freelancer.is_alive == True
    assert freelancer.health == 14    
    priest.heal(freelancer)
    assert freelancer.health == 16

    #battle tests
    my_army = Army()
    my_army.add_units(Defender, 2)
    my_army.add_units(Healer, 1)
    my_army.add_units(Vampire, 2)
    my_army.add_units(Lancer, 2)
    my_army.add_units(Healer, 1)
    my_army.add_units(Warrior, 1)
    
    enemy_army = Army()
    enemy_army.add_units(Warrior, 2)
    enemy_army.add_units(Lancer, 4)
    enemy_army.add_units(Healer, 1)
    enemy_army.add_units(Defender, 2)
    enemy_army.add_units(Vampire, 3)
    enemy_army.add_units(Healer, 1)

    army_3 = Army()
    army_3.add_units(Warrior, 1)
    army_3.add_units(Lancer, 1)
    army_3.add_units(Healer, 1)
    army_3.add_units(Defender, 2)

    army_4 = Army()
    army_4.add_units(Vampire, 3)
    army_4.add_units(Warrior, 1)
    army_4.add_units(Healer, 1)
    army_4.add_units(Lancer, 2)

    army_5 = Army()
	army_5.add_units(Warrior, 10)

	army_6 = Army()
	army_6.add_units(Warrior, 6)
	army_6.add_units(Lancer, 5)

    battle = Battle()

    assert battle.fight(my_army, enemy_army) == False
    assert battle.fight(army_3, army_4) == True
    assert battle.straight_fight(army_5, army_6) == False
    print("Coding complete? Let's try tests!")

if __name__ == '__main__':
    #These "asserts" using only for self-checking and not necessary for auto-testing
    
	ogre = Warrior()
	lancelot = Knight()
	richard = Defender()
	eric = Vampire()
	freelancer = Lancer()
	priest = Healer()

	sword = Sword()
	shield = Shield()
	axe = GreatAxe()
	katana = Katana()
	wand = MagicWand()
	super_weapon = Weapon(50, 10, 5, 150, 8)

	ogre.equip_weapon(sword)
	ogre.equip_weapon(shield)
	ogre.equip_weapon(super_weapon)
	lancelot.equip_weapon(super_weapon)
	richard.equip_weapon(shield)
	eric.equip_weapon(super_weapon)
	freelancer.equip_weapon(axe)
	freelancer.equip_weapon(katana)
	priest.equip_weapon(wand)
	priest.equip_weapon(shield)

	ogre.health == 125
	lancelot.attack == 17
	richard.defense == 4
	eric.vampirism == 200
	freelancer.health == 15
	priest.heal_power == 5

	fight(ogre, eric) == False
	fight(priest, richard) == False
	fight(lancelot, freelancer) == True

	my_army = Army()
	my_army.add_units(Knight, 1)
	my_army.add_units(Lancer, 1)

	enemy_army = Army()
	enemy_army.add_units(Vampire, 1)
	enemy_army.add_units(Healer, 1)

	my_army.units[0].equip_weapon(axe)
	my_army.units[1].equip_weapon(super_weapon)

	enemy_army.units[0].equip_weapon(katana)
	enemy_army.units[1].equip_weapon(wand)

	battle = Battle()

	battle.fight(my_army, enemy_army) == True
    print("Coding complete? Let's try tests!")
