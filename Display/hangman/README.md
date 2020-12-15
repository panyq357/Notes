# Hangman游戏

题目来源：MIT 在 edX 上的 python 课程。

## 解释题目

首先，这个题目的意思是设计一个猜单词游戏。

我先结合示例先介绍一下游戏流程。  

首先，运行ps3_hangman.py。（这不是废话嘛😜）

````cmd
python ps3_hangman.py
````

程序从单词表（就是那个words.txt）里随机抽出一个单词，然后程序告诉玩家单词的长度。

````txt
Loading word list from file...
55900 words loaded.
Welcome to the game, Hangman!
I am thinking of a word that is 4 letters long.
-------------
````

然后程序开始循环询问玩家，让玩家猜单词里的字母。  
猜之前，程序要展示玩家还有几次猜的机会，以及还有那些字母没猜过。  
猜之后，程序要记录玩家的猜测，并告诉玩家是否猜中了。

````txt
You have 8 guesses left.
Available letters: abcdefghijklmnopqrstuvwxyz
Please guess a letter: a
Good guess: _ a_ _
------------
You have 8 guesses left.
Available letters: bcdefghijklmnopqrstuvwxyz
Please guess a letter: a
Oops! You've already guessed that letter: _ a_ _
------------
You have 8 guesses left.
Available letters: bcdefghijklmnopqrstuvwxyz
Please guess a letter: s
Oops! That letter is not in my word: _ a_ _
------------
````

在上面的示例中，程序共循环询问了3次。（如果猜错了，剩余次数就要减1。之后还要循环更多次直到次数用尽。）  

最后，如果玩家在次数用完前猜出了单词里的所有字母。  
程序打印：``Congratulations, you won!``  
反之，程序打印：``Sorry, you ran out of guesses. The word was else.``  

----

## 开始做题

打开 ps_hangman.py 文件，通过阅读注释，我们可以知道，文件里第47行以上的内容（也就是 helper code 框起来的部分，以及 ``wordlist`` 这个全局变量的定义。）都是已经写好的，不需要我们进行修改。

（用 IDLE 打开 .py 文件看不出来哪一行是第47行？用 Visual Studio Code 打开 .py 文件就能看到了。😉）

然后拉到文件的底部，根据注释的说明，我们需要把最后两行取消注释。

````python
# When you've completed your hangman function, uncomment these two lines
# and run this file to test! (hint: you might want to pick your own
# secretWord while you're testing)

secretWord = chooseWord(wordlist).lower()  # 随机获得一个单词（用到的函数就是再 helper code 里定义的）。
hangman(secretWord)  # 把随机获取到的单词作为游戏的答案，并开始游戏。
````

还记得之前的解释 ``if __name__ == "__main__":`` 里提到的 python 版的 ``main()`` 吗？这里 ``hangman()`` 就相当于那个 ``main()``。

既然 ``hangman()`` 是游戏的入口，那就先找到 ``hangman()`` 的定义部分，开始设计吧。

````python
def hangman(secretWord):
    '''
    secretWord: string, the secret word to guess.

    Starts up an interactive game of Hangman.

    * At the start of the game, let the user know how many
      letters the secretWord contains.

    * Ask the user to supply one guess (i.e. letter) per round.

    * The user should receive feedback immediately after each guess
      about whether their guess appears in the computers word.

    * After each round, you should also display to the user the
      partially guessed word so far, as well as letters that the
      user has not yet guessed.

    Follows the other limitations detailed in the problem write-up.
    '''
    # FILL IN YOUR CODE HERE...
````

现在的程序只是一个空壳，一运行起来只会打印两行信息（这两行就是在第46行调用的 ``loadWords()`` 函数打印的）

````text
Loading word list from file...
55900 words loaded.
````

所以我们要先让程序打印一些语句。

然后 ``hangman()`` 就变成这样了。(以下的代码都省略了题目的注释)

````python
def hangman(secretWord):
    print("Welcome to the game, Hangman!")  # 打印欢迎语句。
    print("I am thinking of a word that is {} letters long.".format(len(secretWord)))  # 打印随机单词的长度。
    print("-------------")  # 别忘了分割线。😉
    # TODO
````

接下来要让程序循环询问玩家，由于题目规定“如果用户重复猜了已经猜过的字母，猜测次数不减”，所以循环的次数不是固定的，于是我们不能用 for 循环，得用 while 循环。

在每次循环开始时，我们先要展示有哪些字母没被猜过，这里要调用 ``getAvailableLetters()`` 函数。  

````python
def getAvailableLetters(lettersGuessed):
    # 把列表转换成集合然后进行集合的差运算。
    availableLetters = set(string.ascii_lowercase) - set(lettersGuessed)
    return sorted(availableLetters)  # sorted会自动把集合变回列表。

def hangman(secretWord):
    print("Welcome to the game, Hangman!")
    print("I am thinking of a word that is {} letters long.".format(secretWord))
    print("-------------")
    guessesLeft = 8  # 剩余猜测次数。
    lettersGuessed = []  # 用来装用户输入的字母
    while guessesLeft > 0:
        print("You have {} guesses left.".format(guessesLeft))  # 每轮循环打印剩余次数。
        availableLetters = getAvailableLetters(lettersGuessed)  # 调用getAvailableLetters()。
        print("Available letters: {}".format(''.join(availableLetters)))  # 展示没被猜过的字母。
        # TODO
        print("------------")  # 依然不要忘了分割线。😉
````

接下来要接受用户的输入，并进行以下判断。

1. 用户输入的字母之前输入没？
2. 用户猜对了没？

为此，我们需要编写一些辅助函数（这回是 ``getGuessedWord()``），在 while 循环里编写决策树调用辅助函数。

（注：决策树的编写要小心谨慎，确保没有逻辑混乱的地方。）  
（注2：直接把辅助函数写进决策树里也没错，但是这样就很乱，代码一乱脑子也容易乱了。😂）  

````python
def getGuessedWord(secretWord, lettersGuessed):  # 根据 lettersGuessed 列表给出用于打印的 guessedWord 字符串。
    guessedWord = ['_' for i in range(len(secretWord))]  # 生成一个长度和 secretWord 一样的用下划线填充的列表。
    # 注：上面这种写法叫“列表推导式”，百度一下，你就知道。😉
    for letter in lettersGuessed:  # 对 lettersGuessed 里的每个字母进行检测。
        if letter in secretWord:
            for i in range(len(secretWord)):  # 遍历 secretWord 获取下标。
                if letter == secretWord[i]:  # 用对应位置的字母把下划线替换掉。
                    guessedWord[i] = secretWord[i]
            # 问：你可能还记得字符串有个 .index() 方法可以直接得出单个字符在字符串里的下标，为什么不用它而要用循环呢？
            # 答：因为 .index() 方法只返回第一个匹配的字母，万一单词里有两个"a"就乱了。
    return ' '.join(guessedWord)  # 把修改好的 guessedWord 组装成用空格分隔的字符串，然后返回。



def getAvailableLetters(lettersGuessed):
    availableLetters = set(string.ascii_lowercase) - set(lettersGuessed)
    return sorted(availableLetters)
def hangman(secretWord):
    print("Welcome to the game, Hangman!")
    print("I am thinking of a word that is {} letters long.".format(len(secretWord)))
    print("-------------")
    guessesLeft = 8
    lettersGuessed = []
    while guessesLeft > 0:
        print("You have {} guesses left.".format(guessesLeft))
        availableLetters = getAvailableLetters(lettersGuessed)
        print("Available letters: {}".format(''.join(availableLetters)))
        guess = input("Please guess a letter: ")  # 接受用户的输入。
        if guess not in availableLetters:  # 用户之前输入过这个字母了。
            guessedWord = getGuessedWord(secretWord, lettersGuessed)  # 生成用于打印的像“_ _ a _”这样的 guessedWord 。
            print("Oops! You've already guessed that letter: {}".format(guessedWord))
        else:  # 用户之前没输入过这个字母
            lettersGuessed.append(guess)  # 将这个字母更新进 lettersGuessed 列表。
            guessedWord = getGuessedWord(secretWord, lettersGuessed)  # 用 lettersGuessed 列表生成用于打印的 guessedWord 。
            if guess in secretWord:  # 猜对了
                print("Good guess: {}".format(guessedWord))
            else:  # 猜错了
                print("Oops! That letter is not in my word: {}".format(guessedWord))
                guessesLeft -= 1  # 猜错惩罚，剩余次数减1。

        print("------------")
````

好了，游戏的主体部分已经写完了，现在这个游戏能够记录玩家的输入并作出相应的反映了，但是好像还少了什么。  
对了，判断输赢的规则还没写呢，让我们把最后一点补上。

````python
def isWordGuessed(secretWord, lettersGuessed):  # 判断是否已猜出 secretWord。
    secretWord = list(secretWord)  # 先转换成可删减元素的列表
    for letter in lettersGuessed:  # 检查每个字母
        for i in range(len(secretWord) - 1, -1, -1):  # 反向遍历下标。
            if letter == secretWord[i]:  # 如果 secretWord 中有这个字母。
                secretWord.pop(i)  # 用 .pop() 方法删去这个字母。
        # 问：为什么要反向遍历下标呢？
        # 答：因为要用 .pop() 方法删去字母，如果一个字母被删掉了，它之后的字母的下标也会跟着变。
        # 正向遍历的话，可能就会把某些字母跳过了。
    if secretWord == []:  # 如果 secretWord 被删空了。
        return True
    else:
        return False



def getGuessedWord(secretWord, lettersGuessed):
    guessedWord = ['_' for i in range(len(secretWord))]
    for letter in lettersGuessed:
        if letter in secretWord:
            for i in range(len(secretWord)):
                if letter == secretWord[i]:
                    guessedWord[i] = secretWord[i]
    return ' '.join(guessedWord)



def getAvailableLetters(lettersGuessed):
    availableLetters = set(string.ascii_lowercase) - set(lettersGuessed)
    return sorted(availableLetters)


def hangman(secretWord):
    print("Welcome to the game, Hangman!")
    print("I am thinking of a word that is {} letters long.".format(len(secretWord)))
    print("-------------")
    guessesLeft = 8
    lettersGuessed = []
    while guessesLeft > 0:
        if isWordGuessed(secretWord,lettersGuessed): # 如果已经猜出 secretWord 了。
            print("Congratulations, you won!")
            return  # 直接退出 hangman()。
        print("You have {} guesses left.".format(guessesLeft))
        availableLetters = getAvailableLetters(lettersGuessed)
        print("Available letters: {}".format(''.join(availableLetters)))
        guess = input("Please guess a letter: ")
        if guess not in availableLetters:
            lettersGuessed.append(guess)
            guessedWord = getGuessedWord(secretWord, lettersGuessed)
            print("Oops! You've already guessed that letter: {}".format(guessedWord))
        else:
            lettersGuessed.append(guess)
            guessedWord = getGuessedWord(secretWord, lettersGuessed)
            if guess in secretWord:
                print("Good guess: {}".format(guessedWord))
            else:
                print("Oops! That letter is not in my word: {}".format(guessedWord))
                guessesLeft -= 1

        print("------------")
    print("Sorry, you ran out of guesses. The word was else.")  # 次数用尽了还没猜出来。
    return  # 退出 hangman()。（可写可不写）
````

这下这个游戏总算写好了。(๑•̀ㅂ•́)و✧

## 玩游戏

辛辛苦苦做出来个游戏自己却赢不了一局，这怎么能行。所以让我们用 debug 来作个弊吧。😜

![玩游戏](./LetsPlay.gif)
