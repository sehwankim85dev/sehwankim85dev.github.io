---
title: 버블소트 예제
key: 20181029
tags: bubblesort, today_i_learned
---
~~~
package bubble_sort;

public class BubbleMain implements Runnable {

	BubbleMain() {	}

	public static void main(String[] args) {
		// 스레드 생성을 위해 클래스를 객체화
		BubbleMain bm = new BubbleMain();
		Thread th = new Thread(bm);
		// 스레드 시작
		th.start();
	}

	// 스레드 run() 메서드 오버라이딩
	@Override
	public void run() {
		// 원래 배열
		int[] numbers = { 6, 3, 8, 2, 7, 4, 1, 5 };
        // 총 몇 번의 버블소트가 행해졌는지 나타내는 변수
		int trycount = 0;
        // 메시지를 담을 변수
		String message = "";
        // n번째와 n+1번째를 비교했을 때 n+1번째가 크면
        // 1을 더하는 변수 check
		int check = 0;

		// 원래 배열이 어떻게 되어있는지 보여준다
		for (int x : numbers) {
			System.out.print(x + " ");
		}
		System.out.println(": initial arrangement");
        
		// 버블소트
		for (int i = 0; i < numbers.length; i++) {
			for (int j = 1; j < numbers.length - i; j++) {
            	// 메시지와 check 변수를 반복할 때마다 초기화
				message = "";
				check = 0;
                // j번째 값이 j-1번째 값보다 작으면
                // 자리를 바꾸고 '바뀌었다' 메시지
				if (numbers[j - 1] > numbers[j]) {
					int temp = numbers[j - 1];
					numbers[j - 1] = numbers[j];
					numbers[j] = temp;
					message = "and reverse";
				}
                
                // 콘솔창에 표시하는 부분
                // 알아보기 쉽게 j-1번째와 j번째 양옆으로 괄호를 쳐준다
				for (int n = 0; n < numbers.length; n ++) {
					if (n == j - 1) {
						System.out.print("(" + numbers[n] + " ");
					} else if (n == j) {
						System.out.print(numbers[n] + ") ");
					} else {
						System.out.print(numbers[n] + " ");
					}
				}
                // 각 반복은 0.5초의 간격을 둔다
				try {
					Thread.sleep(500);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
                // j번째와 j-1번째의 숫자가 비교되었음을 출력하고 비교된 두 수가 자리바뀜이 있었다면 바뀌었다는 메시지를 출력한다
				System.out.printf(": compare %dth number(%d) with %dth number(%d) %s\n",
					j-1, numbers[j], j, numbers[j-1], message);
                // 배열의 끝까지 검사했으면 버블소트된 횟수를 1 증가시키고 그 횟수만큼 버블소트 되었다고 출력한다
				if (j + 1 == numbers.length - i) {
					trycount++;
					System.out.printf("%d times Bubble sorted\n\n", trycount);
				}
				// 배열의 모든 자리에서 오름차순 정렬이 이뤄졌는지 검사하고
				for (int k = 1; k < numbers.length; k++) {
					if (numbers[k - 1] < numbers[k]) {
						check++;
					}
				}
				// 총 몇 번의 버블소트가 이뤄진 후에 완전히 오름차순 정렬이 되었는지 출력한다
				if (check == numbers.length - 1) {
					System.out.printf("%d times Bubble sorted. End.\n", ++trycount);
					return;
				}
			}
		}
	}
}

~~~
이클립스 등에 복붙하여 실행해 볼 수 있습니다.
0.5초 간격으로 애니메이션하여 버블소트 과정을 보여주는 코드입니다.