import numpy as np

class Solve_Sudoku:

    def generate(self):
        Board = np.zeros((9, 9), dtype=int)
        Rows = np.full((9, 9), False)
        Cols = np.full((9, 9), False)
        Sqrs = np.full((9, 9), False)
        return (Board, Rows, Cols, Sqrs)

    def initialize(self, Board):
        Rows = np.full((9, 9), False)
        Cols = np.full((9, 9), False)
        Sqrs = np.full((9, 9), False)
        for row in range(9):
            for col in range(9):
                if Board[row, col] != 0:
                    number = Board[row, col]
                    s = self.index_of_square((row, col))
                    Rows[row, number-1] = True
                    Cols[col, number-1] = True
                    Sqrs[  s, number-1] = True
        return (Board, Rows, Cols, Sqrs)
                    
    def index_of_square(self, position):
        return 3 * (position[0] // 3) + (position[1] // 3)
    
    def board_index(self, linear_index):
        return (linear_index // 9, linear_index % 9)

    def place_number(self, Sudoku, position, number): 
        s = self.index_of_square(position)
        if Sudoku[1][position[0], number-1] or Sudoku[2][position[1], number-1] or Sudoku[3][s, number-1]:
            return False
        Sudoku[0][position] = number
        Sudoku[1][position[0], number-1] = True
        Sudoku[2][position[1], number-1] = True
        Sudoku[3][s, number-1] = True
        return True

    def remove_number(self, Sudoku, position, number):
        s = self.index_of_square(position)
        Sudoku[0][position] = 0
        Sudoku[1][position[0], number-1] = False
        Sudoku[2][position[1], number-1] = False
        Sudoku[3][s, number-1] = False
        return None

    def find_solution(self, Sudoku, n): 
        if n == 81:
            return True
        pos = self.board_index(n)
        if Sudoku[0][pos] != 0:
            solved = self.find_solution(Sudoku, n+1)
            return solved
        else:
            for number__1 in range(9):
                if not Sudoku[1][pos[0], number__1]:
                    number_placed = self.place_number(Sudoku, pos, number__1+1)
                    if number_placed: 
                        solved = self.find_solution(Sudoku, n+1)
                        if solved:
                            return True
                        self.remove_number(Sudoku, pos, number__1+1)             
            return False

    def solve_sudoku(self, Unfilled_Sudoku):
        Sudoku = self.initialize(Unfilled_Sudoku)
        solved = self.find_solution(Sudoku, 0)
        if solved:
            Sudoku = Sudoku[0]
            for row in range(9):
                R = ""
                for col in range(9):
                    R = R + " " + str(Sudoku[row, col])
                    if col % 3 == 2:
                        R = R + " |"
                print(R)
                if row % 3 == 2: print(len(R)*"-")
        else:
            print("The sudoku cannot be solved!")
                
            
'''
Application of the sudoku puzzle solver
'''

unfilled_Sudoku_1 = np.array([
[0, 0, 1,   0, 0, 0,   0, 8, 0],
[5, 4, 8,   0, 0, 2,   0, 0, 0],
[9, 0, 0,   0, 1, 0,   7, 0, 0],

[1, 9, 0,   0, 0, 0,   0, 0, 8],
[0, 0, 0,   4, 0, 3,   9, 0, 0],
[2, 0, 0,   0, 0, 0,   0, 5, 0],

[8, 1, 0,   2, 0, 5,   0, 0, 0],
[0, 3, 0,   0, 0, 0,   5, 2, 9],
[6, 0, 2,   0, 9, 0,   0, 0, 1]
])

unfilled_Sudoku_2 = np.array([
[0, 0, 0,   0, 6, 7,   2, 9, 0],
[0, 1, 0,   0, 0, 0,   5, 0, 0],
[7, 0, 6,   0, 0, 0,   0, 0, 8],

[0, 0, 7,   0, 0, 0,   9, 0, 0],
[0, 0, 5,   4, 8, 0,   0, 7, 0],
[0, 4, 0,   0, 0, 0,   0, 5, 2],

[0, 0, 0,   0, 0, 8,   0, 0, 9],
[3, 0, 9,   6, 0, 0,   0, 0, 0],
[5, 2, 0,   0, 4, 0,   0, 3, 1]
])

sudoku_Solver = Solve_Sudoku()
sudoku_Solver.solve_sudoku(unfilled_Sudoku_2)
