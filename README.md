import random
def camel_game():
    print("Welcome to Camel!")
    print("You have stolen a camel to make your way across the great Mobi desert.")
    print("The natives want their camel back and are chasing you down! Survive your")
    print("desert trek and outrun the natives.")
    print()
    # Variables
    done = False
    miles_traveled = 0
    thirst = 0
    camel_tiredness = 0
    natives_distance = -20
    #native start 20 miles behind you
    drinks_in_canteen = 3
    #loop
    while not done:
        print("\nA. Drink from your canteen.")
        print("B. Ahead moderate speed.")
        print("C. Ahead full speed.")
        print("D. Stop for the night.")
        print("E. Status check.")
        print("Q. Quit.")
        user_choice = input("Your choice? ").upper()
        #if we set done to true it will end the game
        if user_choice == "Q":
            done = True
        elif user_choice == "E":
            #status check will tell you all your variables
            print(f"\nMiles traveled: {miles_traveled}")
            print(f"Drinks in canteen: {drinks_in_canteen}")
            print(f"The natives are {miles_traveled - natives_distance} miles behind you.")
        elif user_choice == "D":
            #this resets your camel tiredness because you chose to rest
            camel_tiredness = 0
            print("\nYour camel is happy and rested.")
            #natives will slowly catch up while resting
            natives_distance += random.randint(7, 14)
        elif user_choice == "C":
            miles = random.randint(10, 20)
            miles_traveled += miles
            #you will gain thirst every move having 6 will make you die
            thirst += 1
            #running full speed will make your camel more tired than moderate speed
            camel_tiredness += random.randint(1, 3)
            #natives will catch up
            natives_distance += random.randint(7, 14)
            print(f"\nYou traveled {miles} miles.")
        elif user_choice == "B":
            #you move slower for the benifit of getting less tired
            miles = random.randint(5, 12)
            miles_traveled += miles
            thirst += 1
            camel_tiredness += 1
            natives_distance += random.randint(7, 14)
            print(f"\nYou traveled {miles} miles.")
        elif user_choice == "A":
            if drinks_in_canteen > 0:
                #you loose a drink everytime you use one
                drinks_in_canteen -= 1
                thirst = 0
                print("\nYou take a drink from your canteen.")
            else:
                print("\nYou have no drinks left!")
        if thirst > 6:
            print("You died of thirst!")
            done = True
        elif thirst > 4:
            print("You are thirsty.") 
        if camel_tiredness > 8:
            print("Your camel is dead.")
            done = True
        elif camel_tiredness > 5:
            print("Your camel is getting tired.")
        #if the natives distance is greater then the distance you traveled the game will end
        if natives_distance >= miles_traveled:
            print("The natives have caught up to you!")
            done = True
        elif miles_traveled - natives_distance < 15:
            print("The natives are getting close!")
        if miles_traveled >= 200:
            print("Congratulations, you have crossed the desert and won!")
            done = True
        #theres a 1 in 20 chance you get an oasis, the oasis makes you have no thirst, tiredness, and gives you another 3 drinks in your canteen
        if not done and random.randint(1, 20) == 1:
            print("You found an oasis! You refill your canteen and rest your camel.")
            drinks_in_canteen = 3
            thirst = 0
            camel_tiredness = 0
camel_game()
