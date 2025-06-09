# Nba-Quiz-with-python
My end of year python 2 project. This a a quiz in which the user inputs a player name and you take a 5 question quiz over said player.


#Import Libraries 

pip requests
import requests

#Variables 

iteration = 0

active = False

active_l = []
team_l = []
nationality_l = []
position_l =[]

question = tsapp.TextLabel("BlackOpsOne-Regular.ttf", 30, 0, 0, 500, "", tsapp.BLACK)

points = 0

player_ids = []

## -- API Constants -- ##

BASE_URL = "https://www.thesportsdb.com/api/v1/json"
API_KEY = "3"


player = input("What basketball player do you want to take a quiz over? ")

while True:

    if iteration > 0:
        player = input("Try searching again: ")
    iteration += 1

#### ---- API CALL ---- ####

    request_url = BASE_URL + "/" + API_KEY + "/searchplayers.php"
    parameters = {"p": player, "strSport": "Basketball"}
    response = requests.get(request_url, params=parameters)

    body = response.json()

    basketball_players = []

    #Check for basketball players
    for result in body["player"]:
        if result["strSport"] == "Basketball":
            basketball_players.append(result["strPlayer"])
            team_l.append(result["strTeam"])
            active_l.append(result["strStatus"])
            nationality_l.append(result["strNationality"])
            position_l.append(result["strPosition"])

    if len(basketball_players) == 1:
        choice = basketball_players[0]
        team = team_l[0]
        nationality = nationality_l[0]
        if active_l[0] == "Active":
            active = True
        position = position_l[0]
        break
        
        break
        
    elif len(basketball_players) > 1:
        print()
        print(basketball_players)
        print()
    selected = input("Which one? (\"none\" or 1, 2, 3...): ")
    
    if selected.lower() == "none":
        continue
    else:
        try:
            index = int(selected) - 1
            choice = basketball_players[index]
            team = team_l[index]
            nationality = nationality_l[index]
            if active_l[index] == "Active":
                active = True
            position = position_l[index]
            break
        except (IndexError, ValueError):
            print("Invalid selection. Try again.\n")
            continue
else:
    print("Invalid input.\nMaybe try adding a last name or first name.\n")
    
    
print("\n" + choice)

if team == "_Retired Basketball":
    team = "Retired"

#### ---- OUTPUT ---- ####

print("")

#Window

#TEXT

print( "FORMATING\n-----------\nCapitalize the begining of each world\nex.Shooting Guard, Dallas Mavericks\nIf they are retired, guess \"Retired\" for the team")
window.add_object(text)
text.align = "center"

itteration = 0

#Main Loop

while True:
    correct = False
    
    #Questions
    
    if itteration == 0:
        print("What team does he play for?")
        team_g = input("Your guess: ")
        if team_g == team:
            correct = True
        else:
            print("The Correct Answer Was " + team)
            input()
        
    elif itteration == 1:
        print("What country is he from?")
        nationality_g = input("Your guess: ")
        if nationality_g == nationality:
            correct = True
        else:
            print("The Correct Answer Was " + nationality)
            input()
        
    elif itteration == 2:
        print("Is he in the league currently? \"y\" or \"n\"")
        active_g = input("Your guess: ") == "y"
        if (active_g and active) or (not active_g and not active):
            correct = True
        else:
            print("The Correct Answer Was " + str(active))
            input()
            
    elif itteration == 3:
        print("What position is he? ")
        position_g = input("Your guess: ")
        if position_g == position:
            correct = True
        else:
            print("The Correct Answer Was " + position)
            input()
    
    else:
        if points < 4:
            print("You got " + str(points) + " questions out of 4")
            input()
            break
        else:
            print("You got " + str(points) + " questions out of 4")
            input()
            break
    
    #Check if input was correct
    
    if correct:
        points += 1
        print("Correct!")
        input()
        
    itteration += 1

