# NumberBaseballGame
```python
Java Number Baseball Game

package project;

import java.util.*;

public class NumberBaseballGame {

    static Scanner sc = new Scanner(System.in);
    static Random random = new Random();

    public static void main(String[] args) {

        System.out.println("=============================");
        System.out.println(" 숫자 야구 게임에 오신 것을 환영합니다!");
        System.out.println("=============================");

        boolean restart = true;

        while (restart) {

            // 난이도 설정
            int digit = 3;
            int maxTry = -1;

            System.out.println("\n난이도를 선택하세요.");
            System.out.println("1. 쉬움 (Easy)");
            System.out.println("2. 보통 (Normal)");
            System.out.println("3. 어려움 (Hard)");
            System.out.print("선택 >> ");

            int level = inputDifficulty();

            switch (level) {
                case 1:
                    digit = 4;
                    maxTry = -1;
                    break;

                case 2:
                    digit = 3;
                    maxTry = -1;
                    break;

                case 3:
                    digit = 3;
                    maxTry = 10;
                    break;
            }

            // 정답 생성
            int[] answer = createAnswer(digit);

            int tryCount = 0;
            boolean clear = false;

            System.out.println("\n[게임 시작] 서로 다른 숫자 " + digit + "개를 맞춰보세요!");

            while (true) {

                if (maxTry != -1) {
                    System.out.println("(남은 기회 : " + (maxTry - tryCount) + "회)");
                }

                int[] user = inputNumbers(digit);

                tryCount++;

                int strike = 0;
                int ball = 0;

                // 판정
                for (int i = 0; i < digit; i++) {
                    for (int j = 0; j < digit; j++) {

                        if (user[i] == answer[j]) {

                            if (i == j) {
                                strike++;
                            } else {
                                ball++;
                            }
                        }
                    }
                }

                // 결과 출력
                if (strike == 0 && ball == 0) {
                    System.out.println("결과 : Out");
                } else {
                    System.out.println("결과 : " + strike + " Strike " + ball + " Ball");
                }

                // 정답 처리
                if (strike == digit) {
                    clear = true;
                    System.out.println("\n🎉 정답입니다!");
                    System.out.println("총 시도 횟수 : " + tryCount + "회");
                    break;
                }

                // 어려움 난이도 실패 처리
                if (maxTry != -1 && tryCount >= maxTry) {

                    System.out.println("\n💀 게임 오버!");
                    System.out.print("정답 : ");

                    for (int n : answer) {
                        System.out.print(n + " ");
                    }

                    System.out.println();
                    break;
                }
            }

            // 재시작 여부
            System.out.print("\n다시 하시겠습니까? (Y/N) >> ");

            String again = sc.next().toUpperCase();

            if (!again.equals("Y")) {
                restart = false;
            }
        }

        System.out.println("\n게임을 종료합니다.");
    }

    // 난이도 입력
    public static int inputDifficulty() {

        while (true) {

            try {

                int level = sc.nextInt();

                if (level >= 1 && level <= 3) {
                    return level;
                } else {
                    System.out.print("1~3 사이 숫자를 입력하세요 >> ");
                }

            } catch (InputMismatchException e) {

                System.out.print("숫자만 입력하세요 >> ");
                sc.nextLine();
            }
        }
    }

    // 정답 생성
    public static int[] createAnswer(int digit) {

        int[] answer = new int[digit];
        boolean[] used = new boolean[10];

        for (int i = 0; i < digit; i++) {

            int num;

            while (true) {

                num = random.nextInt(9) + 1;

                if (!used[num]) {
                    used[num] = true;
                    break;
                }
            }

            answer[i] = num;
        }

        return answer;
    }

    // 사용자 입력
    public static int[] inputNumbers(int digit) {

        while (true) {

            try {

                int[] numbers = new int[digit];
                boolean[] used = new boolean[10];

                System.out.print("\n숫자 " + digit + "개를 입력하세요 >> ");

                for (int i = 0; i < digit; i++) {

                    int num = sc.nextInt();

                    // 범위 검사
                    if (num < 1 || num > 9) {
                        throw new IllegalArgumentException("숫자는 1~9 사이만 가능합니다.");
                    }

                    // 중복 검사
                    if (used[num]) {
                        throw new IllegalArgumentException("중복된 숫자는 입력할 수 없습니다.");
                    }

                    used[num] = true;
                    numbers[i] = num;
                }

                return numbers;

            } catch (InputMismatchException e) {

                System.out.println("오류 : 숫자만 입력하세요.");
                sc.nextLine();

            } catch (IllegalArgumentException e) {

                System.out.println("오류 : " + e.getMessage());
                sc.nextLine();
            }
```
        }
    }
}
