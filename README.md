movie20Qs
=========
def mQuestions():
    key = []
    questions = open("movieQuestions.txt", "r")
    data = questions.readlines()
    questions.close()

    for x in range(len(data)):
        key.append(input("Y=1/N=0",data[x]))
    return key

def addMovie(key,index,movie):
    newMovie1 = input("Your Movie Is Not In Our System. Please Enter Your Movie")

    newMovie2 = newMovie1.replace(" ","-")
    for x in range(len(movie)):
        if newMovie2 == movie[x]:
            return 1
    nMovie = open("movieKey.txt", "a")

    last = len(index)+1
    addedMovie = (newMovie2+" "+str(last)+" "+key)
    nMovie.write("\n"+addedMovie)

    nMovie.close()

    return newMovie2

def check(movie,code,key,index):
    for x in range(len(movie)):
        if key == code[x]:
            return movie[x]
    return 0
def checkRepeats(code):
    count = 0
    repeats = 0
    for x in range(len(code)):
        if code[count] == code[x] and count != x:
            repeats = repeats + 1
        count = count + 1
    return repeats
def movieLookUp(key):
    key = "".join(key)
    movie = []
    index = []
    code = []
    movieKey = open("movieKey.txt", "r")

    data = movieKey.readline()
    while( data != "" ):
        line = data.split()
        movie.append(line[0])
        index.append(line[1])
        code.append(line[2])
        data = movieKey.readline()

    movieKey.close()
    yourMovie = check(movie,code,key,index)
    if yourMovie == 0:
        print("No Repeats: ",checkRepeats(code))
        if addMovie(key,index,movie) == 1:
            return 1
        else:
            return 0
    else:
        return yourMovie

def interface():
    print("Welcome to 20 Questions: Movie Edition\nThink of a movie...\n")
    key = mQuestions()
    nKey = []
    for x in range (len(key)):
        s = str(key[x])
        nKey.append(s)
    yourMovie = movieLookUp(nKey)
    if yourMovie == 0:
        print("Your Movie Has Been Added")
    elif yourMovie == 1:
        print("You don't know your movie. Go watch it again!")
    else:
        movieF = input("Is {0} the movie you were thinking of...Y=1/N=0".format(yourMovie))
        if movieF == "1":
            print("coolio")
        else:
            print("damn")
interface()
