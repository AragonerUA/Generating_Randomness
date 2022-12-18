import random


class GenerateRandomness:
    """Generate Randomness"""
    def __init__(self):
        self.string_for_learning = ""  # string for AI to learn
        self.data_dictionary = {"000": [0, 0], "001": [0, 0], "010": [0, 0], "011": [0, 0],
                                "100": [0, 0], "101": [0, 0], "110": [0, 0], "111": [0, 0]}
        self.test_string = ""  # test string for making prediction

        self.predicted_string = ""  # string that was predicted by AI
        self.result_string = ""  # output string that contains statistics about the AI prediction

        self.balance = 1000  # balance for our game

    """Menu function for game"""
    def menu(self):
        print("Please give AI some data to learn...")
        print("The current data length is", len(self.string_for_learning), ",", 100-len(self.string_for_learning),
              "symbols left")
        GenerateRandomness.get_data_from_user(self)
        print("You have $" + str(self.balance) + "." +
              " Every time the system successfully predicts your next press, you lose $1.")
        print('Otherwise, you earn $1. Print "enough" to leave the game.' + " Let's go!\n")
        GenerateRandomness.count_triads(self)
        GenerateRandomness.prediction(self)

    def get_data_from_user(self):
        while len(self.string_for_learning) < 100:
            input_string = input("Print a random string containing 0 or 1:\n\n")
            self.string_for_learning += GenerateRandomness.cleaning_string(input_string)
            if len(self.string_for_learning) < 100:
                print("The current data length is", len(self.string_for_learning), ",",
                      100-len(self.string_for_learning), "symbols left")
        print("Final data string:", self.string_for_learning, sep="\n", end="\n\n")

    def balance_counting(self):
        print("Your balance is now $" + str(self.balance), end="\n\n")

    @staticmethod
    def cleaning_string(string):
        cleaned_string = ""
        for i in string:
            if (i == "0") or (i == "1"):
                cleaned_string += i
        return cleaned_string

    def count_triads(self):
        for i in range(len(self.string_for_learning)-3):
            k = self.string_for_learning[i:i+3]
            if self.string_for_learning[i+3] == "0":
                self.data_dictionary[k][0] += 1
            elif self.string_for_learning[i+3] == "1":
                self.data_dictionary[k][1] += 1

    def beautiful_dict_print(self):
        for i, j in self.data_dictionary.items():
            print(str(i)+":", str(j[0])+","+str(j[1]))

    def prediction(self):
        while True:
            test_string = input("Print a random string containing 0 or 1:\n")
            if test_string == "enough":
                print("Game over!", end="")
                break
            test_string = GenerateRandomness.cleaning_string(test_string)
            if len(test_string) != 0:
                self.test_string = GenerateRandomness.cleaning_string(test_string)
            else:
                print()
                continue
            self.predicted_string = str(random.randint(0, 1)) + str(random.randint(0, 1)) + str(random.randint(0, 1))
            for i in range(len(self.test_string)-3):
                pattern = self.test_string[i:i+3]
                if self.data_dictionary[pattern][0] > self.data_dictionary[pattern][1]:
                    self.predicted_string += str(0)
                elif self.data_dictionary[pattern][0] < self.data_dictionary[pattern][1]:
                    self.predicted_string += str(1)
                else:
                    self.predicted_string += str(random.randint(0, 1))
            N = 0
            for i in range(3, len(self.test_string)):
                if self.test_string[i] == self.predicted_string[i]:
                    N += 1
            self.balance -= N
            self.balance += ((len(self.test_string)-3) - N)
            self.result_string = "Computer guessed right " + str(N) + " out of " + str(len(self.test_string)-3) +\
                                 " symbols " + "(" + str(round(N/(len(self.test_string)-3)*100, 2)) + " %)"
            print("prediction:", self.predicted_string + "\n", self.result_string, sep="\n")
            GenerateRandomness.balance_counting(self)


if __name__ == "__main__":
    GenerateRandomness().menu()
