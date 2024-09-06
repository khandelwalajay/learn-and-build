# learn-and-build
//MazeSolver

import java.util.LinkedList;
import java.util.Queue;

public class MazeSolver {
    static final int N = 5;

    static class Point {
        int x, y;
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    static boolean isSafe(int[][] maze, int x, int y) {
        return (x >= 0 && x < N && y >= 0 && y < N && maze[x][y] == 1);
    }

    static boolean solveMaze(int[][] maze) {
        int[][] solution = new int[N][N];
        Queue<Point> queue = new LinkedList<>();
        queue.add(new Point(0, 0));
        solution[0][0] = 1;

        int[] row = { -1, 0, 0, 1 };
        int[] col = { 0, -1, 1, 0 };

        while (!queue.isEmpty()) {
            Point point = queue.poll();
            int x = point.x;
            int y = point.y;

            if (x == N - 1 && y == N - 1) {
                printSolution(solution);
                return true;
            }

            for (int i = 0; i < 4; i++) {
                int newX = x + row[i];
                int newY = y + col[i];

                if (isSafe(maze, newX, newY) && solution[newX][newY] == 0) {
                    queue.add(new Point(newX, newY));
                    solution[newX][newY] = 1;
                }
            }
        }
        return false;
    }

    static void printSolution(int[][] solution) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                System.out.print(" " + solution[i][j] + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int[][] maze = {
            { 1, 0, 0, 0, 0 },
            { 1, 1, 0, 1, 0 },
            { 0, 1, 0, 0, 0 },
            { 0, 1, 1, 1, 1 },
            { 0, 0, 0, 0, 1 }
        };

        if (!solveMaze(maze)) {
            System.out.println("No solution exists");
        }
    }
}
