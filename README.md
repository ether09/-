# -package bug20221281;

import java.util.Scanner;
import java.util.Random;

public class bug20221281 {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        int playerHP = 100;
        int playerLevel = 1;
        int monsterHP = 30;
        int round = 1;
        
        int maxPlayerHP = 100;
        
        String[] choices = {"가위", "바위", "보"};

        System.out.println("==== 가위바위보 RPG 게임 시작 ====");

        while (playerHP > 0) {
            System.out.println("\n[Round " + round + "] 몬스터 체력: " + monsterHP + " / 당신 체력: " + playerHP);
            System.out.print("가위(1), 바위(2), 보(3) 중 선택하세요: ");
            int playerChoice = scanner.nextInt();
            int monsterChoice = random.nextInt(3) + 1;

            System.out.println("당신의 선택: " + choices[playerChoice - 1]);
            System.out.println("몬스터의 선택: " + choices[monsterChoice - 1]);

            int damage = 10 + playerLevel * 2;

            if (playerChoice == monsterChoice) {
                System.out.println("비겼습니다!");
            } else if ((playerChoice == 1 && monsterChoice == 3) ||
                       (playerChoice == 2 && monsterChoice == 1) ||
                       (playerChoice == 3 && monsterChoice == 2)) {
                System.out.println("이겼습니다! 몬스터에게 " + damage + " 데미지를 입혔습니다.");
                monsterHP -= damage;
            } else {
                System.out.println("졌습니다! 몬스터에게 공격당했습니다.");
                playerHP -= 10 + random.nextInt(5);
            }

            if (monsterHP <= 0) {
                System.out.println("몬스터를 쓰러뜨렸습니다! 레벨 업!");
                playerLevel++;
                playerHP = Math.min(playerHP + 20, maxPlayerHP);
                monsterHP = 30 + playerLevel * 10;
                round++;
            }

            if (playerHP <= 0) {
                System.out.println("당신은 쓰러졌습니다... 게임 오버.");
                break;
            }
        }

        scanner.close();
    }
}
