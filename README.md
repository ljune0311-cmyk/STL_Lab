# STL_Lab
공부용/학습용
# 프로그램 실습 코드
### vector class

1. 다음과 같이 int형 ``vector`` 클래스의 객체를 선언하고 객체에 새로운 데이터를 ``push_back()`` 을 여러번 호출하도록 코드를 수정하라. ``push_back()`` 함수를 호출할 때 마다 객체에 대해 size와 capacity를 구해서 값의 변화를 분석하라
```c++
#include <iostream>
#include <vector>
using namespace std;
int main(int argc, char const* argv[])
{
	vector <int> v1;
	v1.push_back(10);
	cout << "size: " << v1.size() << " " << "capacity: " << v1.capacity() << endl;
	v1.push_back(20);
	cout << "size: " << v1.size() << " " << "capacity: " << v1.capacity() << endl;
	v1.push_back(30);
	cout << "size: " << v1.size() << " " << "capacity: " << v1.capacity() << endl;
	v1.push_back(40);
	cout << "size: " << v1.size() << " " << "capacity: " << v1.capacity() << endl;
	v1.push_back(50);
	cout << "size: " << v1.size() << " " << "capacity: " << v1.capacity() << endl;
	v1.push_back(60);
	cout << "size: " << v1.size() << " " << "capacity: " << v1.capacity() << endl;

	//size()
	//	백터에 실제로 들어 있는 원소의 개수를 반환한다.
	//	현재 백터가 사용 중인 메모리 크기이다.
	//	capacity()
	//	벡터가 현재 재할당 없이 저장할 수 있는 최대 원소 수를 반환한다.
	//	벡터에 미리 확보한 메모리 공간의 크기이다.이 값은 size보다 크거나 같다.
	//	->재할당이란 push_back()등 같이 원소를 추가할 때 size가 capacity와 같아지면 새 공간을 할당한다.
}
```

2. 클래스 템플릿 ``vector``를 사용한 프로그램이다. 프로그램 수행 결과를 예측하고 실행 결과의 비교하고 vector 분석하라.

```c++
#include <vector>
#include <iostream>
using namespace std;
int main()
{
    vector<int> v1, v2, v3;

    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    v1.push_back(40);
    v1.push_back(50);

    cout << "v1 = ";
    for (auto& v : v1) {
        cout << v << " ";
    }
    cout << endl;

    v2.assign(v1.begin(), v1.end());
    cout << "v2 = ";
    for (auto& v : v2) {
        cout << v << " ";
    }
    cout << endl;

    v3.assign(3, 6);
    cout << "v3 = ";
    for (auto& v : v3) {
        cout << v << " ";
    }
    cout << endl;

    v3.assign({ 5, 6, 7 });
    for (auto& v : v3) {
        cout << v << " ";
    }
    cout << endl;

    int& i = v1.at(0);

    cout << "v1 첫 번째 원소의 값:  " << i << endl;

    if (v1 == v2) cout << "v1과 v2는 같다." << endl;
    else cout << "v1과 v2는 다르다" << endl;

    i = 80;
    const int& j = v1.at(0);

    cout << "값을 변경 후 v1 첫 번째 원소의 값:  " << j << endl;

    if (v1 == v2) cout << "v1과 v2는 같다." << endl;
    else cout << "v1과 v2는 다르다" << endl;

    //v1은 벡터의 모든 원소를 출력, v2는 assign()를 사용하여 v1의 값을 복사하여 채워넣었다.
    //    v3(3, 6)은 assign() 함수를 통해 크기가 3인 벡터를 만들고 모든 원소를 6으로 채웠다.->함수 오버로드
    //    v3({ 5,6,7 })은 초기화 리스트를 사용해서 벡터를 채웠다.
}
```

3. 사각형을 표현하는 클래스를 정의하고 클래스를 ``vector`` 를 이용하여 저쟝하고 처리하는 프로그램을 작성하라.
```c++
#include <iostream>
#include <vector>
using namespace std;

// 사각형 클래스 정의
class Rect {
	int width;
	int height;

public:
	Rect(int w, int h) : width(w), height(h){}

	int area() {
		return width * height;
	}

	void print() {
		cout << "가로: " << width << ", 세로: "
			<< height << ", 면적: " << area() << endl;
	}
};

int main()
{
	// Rect 객체들을 저장할 vector
	vector<Rect> rects;

	// 사각형 저장
	rects.push_back(Rect(3, 4));
	rects.push_back(Rect(10,2));
	rects.push_back(Rect(5, 5));

	//출력
	for (Rect& r : rects) { r.print(); }
	
	return 0;
}
```

4. 다음 프로그램의 실행 결과를 분석하라.

```c++
#include <vector>
#include <iostream>
using namespace std;
int main()
{
	vector<int> v1(5);
	v1.push_back(3);

//6. 4의 프로그램에서 첫 번째 위치에 데이터 10을 저장하는 프로그램을 작성하라.
	v1[0] = 10;
	for (int i : v1) {cout << i << " ";}
	cout << endl;

	cout << v1.capacity() << endl;
	cout << v1.size() << endl;
}

//4. 다음 프로그램의 실행 결과를 분석
//vector<int> v1(5)를 생성하면 일단 벡터는 클래스 템플릿이기 때문에 생성자를 통해 크기가 5인 벡터를 생성하며, size와 capacity는 최소 5가 된다.
//push_back(3)을 호출하면 새 요소를 추가하기 때문에
//size는 6이 되며, capacity는 재할당을한다.
//capacity는 정확하지 않지만 보통 두 배로 공간을 할당하기 때문에 10이라고 일단 추론해 볼 수 있다.
```

5.  4번의 프로그램에서 3 저장되는 위치는?
```
push_back()은 기존 요소에 새로운 요소를 마지막 요소에 추가하므로 마지막 요소에 3이 저장된다.
```

6.  4의 프로그램에서 첫 번째 위치에 데이터 10을 저장하는 프로그램을 작성하라.


7. 아래의 링크를 참조하여 vector 클래스의 다른 멤버 함수와 연산자를 활용한 프로그램을 작성하라.
https://learn.microsoft.com/ko-kr/cpp/standard-library/vector-operators?view=msvc-170 
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main()
{
	// 정수형 벡터 v1,v2생성
	vector<int> v1{ 1,2,3,4,5 };
	vector<int> v2{ 5,4,3,2,1 };

	// 출력
	cout << "v1 원소 출력: ";
	for (int i : v1) { cout << i << " "; }
	cout << "\n";

	cout << "v2 원소 출력: ";
	for (int i : v2) { cout << i << " "; }
	cout << "\n\n";

	// sort() 함수로 벡터 v2 정렬
	sort(v2.begin(), v2.end());

	cout << "정렬된 v2 원소 출력: ";
	for (int i : v2) { cout << i << " "; }
	cout << "\n\n";

	if (v1 == v2) { cout << "두 벡터는 같음"; }
	else { cout << "두 벡터는 다름"; }
	cout << "\n";

	if (v1 <= v2) { cout << "벡터 v1은 벡터 v2보다 작거나 같다"; }
	else { cout << " 벡터 v1은 벡터 v2보다 크다"; }
	cout << "\n\n";

	v1.push_back(6);
	cout << "v1.push_back(6)으로 추가 후\n";
	cout << "v1 원소 출력: ";
	for (int i : v1) { cout << i << " "; }
	cout << "\n";
	cout << "v2 원소 출력: ";
	for (int i : v2) { cout << i << " "; }
	cout << "\n";

	if (v1 <= v2) { cout << "벡터 v1은 벡터 v2보다 작거나 같다"; }
	else { cout << "벡터 v1은 벡터 v2보다 크다"; }
}

//v1과 v2 벡터를 생성하고 v1은 오름차순된 원소를 벡터에 넣고 v2는 내림차순된 원소를 벡터에 넣는다.
//sort(v2.begin(), v2.end())를 통해 v2의 원소를 오름차순으로 정렬하였고 추가로 push_back으로 v1에 6을 추가하였다.
//v1과 v2을 operator <=와 operator==를 이용해서 비교한 코드이다.
```

8. SampleCodes/STL 디렉토리의 ``vector_sample.cc`` 파일을 기반으로 ``vector`` 클래스의 멤버 함수를 검증하는 함수를 작성하라.

```c++
#include <iostream>
#include <vector>
using namespace std;


//

void assignTest() {
    vector <int> v1, v2, v3, v4;

    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    v1.push_back(40);
    v1.push_back(50);

    cout << "the value of elements of v1 " << endl;
    for (auto& e : v1) cout << e << ",";
    cout << endl;
    cout << "the capacity of v1: " << v1.capacity() << endl;
    cout << "the value of elements of v2 after assign" << endl;
    v2.assign(v1.begin(), v1.end());

    cout << "the size of v2: " << v2.size() << endl;
    cout << "the capacity of v2: " << v2.capacity() << endl;

    for (auto& e : v1) cout << e << ",";
    cout << endl;

    v3.assign(10, 3);
    cout << "the result of v3.assign(7 , 3): " << endl;
    cout << "the size of v3: " << v3.size() << endl;
    cout << "the capacity of v3: " << v3.capacity() << endl;

    for (auto& e : v3) cout << e << ", ";
    cout << endl;

    v4.assign({ 5, 6, 7, 8 });
    cout << "the result of v4.assign({5, 6, 7}): " << endl;
    cout << "the size of v4: " << v4.size() << endl;
    cout << "the capacity of v4: " << v4.capacity() << endl;

    for (auto& e : v4) cout << e << ", ";
    cout << endl;

}

void itrTest() {
    vector <int> v1;
    vector <int>::iterator v1_itr;
    vector <int>::const_iterator v1_citer;

    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    v1.push_back(40);
    v1.push_back(50);

    v1_itr = v1.begin();
    cout << "Access the data through the iterator" << endl;
    for (; v1_itr != v1.end(); v1_itr++) cout << *v1_itr << ", ";
    cout << endl;

    v1_itr = v1.begin();
    cout << "Add 100 to every element in the vector through the iterator" << endl;
    for (; v1_itr != v1.end(); v1_itr++) *v1_itr += 100;

    cout << "Accee the element with range-for loop in the vector" << endl;
    for (auto& e : v1) cout << e << ", ";
    cout << endl;

    cout << "Accee the element with for loop in the vector" << endl;
    for (int i = 0; i < v1.size(); i++) cout << v1[i] << ", ";
    cout << endl;
}

void sizeTest() {
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    cout << "size of vector: " << v1.size() << endl;
}

void capacityTest() {
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    cout << "capacity of vector: " << v1.capacity() << endl;
}

void atTest() {
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);

    int& e = v1.at(1);

    cout << e << endl;
    e = 60;
    cout << v1[1] << endl;

}

void backTest()
{
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);  
    cout << "backTest [맨 마지막 요소를 반환]: " << v1.back() << endl;
}

void beginTest()
{
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    auto a = v1.begin();
    cout << "beginTest [맨 첫번째 요소를 가리킴]: " << * a << endl;
}

void endTest()
{
    vector <int> v1;
    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    auto e = v1.end();

    cout << "end - begin: " << (e - v1.begin()) << endl;
    if (e == v1.begin() + v1.size()) {
        cout << "endTest [맨 마지막 요소의 다음위치를 가리킴]" << endl;
    }
    else cout << "다음 위치를 가리키지 않음" << endl;
}

void clearTest()
{
    vector <int> v1(10, 1);
    cout << "clearTest [Vector의 내부를 초기화] " << endl;
    cout << "[Before] size: " << v1.size() << " capacity: " << v1.capacity() << endl;
    v1.clear();
    cout << "[After] size: " << v1.size() << " capacity : " << v1.capacity() << endl;
    for (auto i : v1) { cout << i << " "; } // 출력 안됨 -> size가 0이기 때문
}

int main(int argc, char const* argv[])
{
    backTest();
    cout << endl;
    beginTest();
    cout << endl;
    endTest();
    cout << endl;
    clearTest();
    return 0;
}
```

## 프로그램 문제
1. 다음 프로그램을 main 함수 내에 작성하라.
  * 키보드로부터 정수가 0이 입력될 때 까지 정수를 입력받아 vector 컨테이너에 저장하는 프로그램을 작성하라. (vector 컨테이너에 0은 저장하지 않음)
  * 키보드로 부터 입력된 정수의 개수를 vector의 멤버함수를 이용하여 구하는 프로그램을 작성하라.
  * vector에 저장된 정수들의 평균을 구하는 프로그램을 작성하라.
  * vector에 저정된 정수들을 같은 정수 값이 몇 개가 입력되었는지 출력하는 프로그램을 작성하라. 

  ```c++
  #include <iostream>
#include <vector>
using namespace std;

int main() {

	// 키보드로부터 정수가 0이 입력될 때 까지 정수를 입력받아 vector 컨테이너에 저장하는 프로그램
	int scan;
	vector <int> v;
	while (true)
	{
		cin >> scan;
		if (scan == 0) { break; }
		else {
			v.push_back(scan);
	//vector에 저정된 정수들을 같은 정수 값이 몇 개가 입력되었는지 출력하는 프로그램을 작성하라.
			int c = count(v.begin(), v.end(), scan);
			cout << scan << " : " << c << "개" << endl;
		}
	}
	cout << endl;
	for (auto a : v) {
		cout << a << " ";
	}
	// 키보드로 부터 입력된 정수의 개수를 vector의 멤버함수를 이용하여 구하는 프로그램을 작성하라.
	cout << endl;
	cout <<"정수의 개수: " << v.size() << endl;

	// vector에 저장된 정수들의 평균을 구하는 프로그램을 작성하라.
	int sum = 0;
	for (int a : v) {
		sum += a;
	}
	cout <<"평균: " << sum / v.size() << endl;


	return 0;
}
```

2. 다음 프로그램을 main 함수 내에 작성하라. 
  * 키보드로 부터 입력된 정수 값을 key로 하고 각 입력된 정수의 중복 개수를 값으로 저장하는 map을 구현하는 프로그램을 작성하라.
  * 키보드로 부터 입력된 정수의 개수를 map의 멤버함수를 이용하여 구하는 프로그램을 작성하라.
  * map에 저장된 정수들의 평균을 구하는 프로그램을 작성하라.
  * map에 저정된 정수들을 같은 정수 값이 몇 개가 입력되었는지 출력하는 프로그램을 작성하라.

  ```c++
  #include <iostream>
#include <vector>
#include <algorithm>
#include <map>

using namespace std;

int main()
{
	// 키보드로 부터 입력된 정수 값을 key로 하고 각 입력된 정수의 중복 개수를 값으로 저장하는 map을 구현하는 프로그램
	map<int, int> countMap;
	int m;
	while (true)
	{
		cin >> m;
		if (m == 0) { break; }
		countMap[m]++;
	}

	// map에 저정된 정수들을 같은 정수 값이 몇 개가 입력되었는지 출력하는 프로그램을 작성
	cout << "정수의 중복 개수" << endl;
	for (auto a = countMap.begin(); a != countMap.end(); ++a) {
		cout << "정수 " << a->first << " " << a->second << "개" << endl;
	}

	// 키보드로 부터 입력된 정수의 개수를 map의 멤버함수를 이용하여 구하는 프로그램
	cout << "정수의 개수: " << countMap.size() << endl;

	// map에 저장된 정수들의 평균을 구하는 프로그램
	int sum = 0;

	for (auto a = countMap.begin(); a != countMap.end(); ++a) {
		sum += a->first;
	}
	cout << "평균: " << sum / countMap.size() << endl;

	return 0;
}
```
3. 다음 프로그램을 main 함수 내에 작성하라.     
  * 키보드로 부터 이름(string)(key)과 전화번호(string)(value)입력 받아 저장하는 것을 map을 이용하여 구현하는 프로그램을 작성하라.
  * 특정 이름에 대해서 전화번호를 출럭하는 프로그램을 작성하라.

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <map>
using namespace std;

int main() {
	// 키보드로 부터 이름(string)(key)과 전화번호(string)(value)입력 받아 저장하는 것을 map을 이용하여 구현하는 프로그램
	map<string, string> numberMap;
	string name, number;
	while (true)
	{
		cout << "이름: ";
		cin >> name;
		if (name == "0") { break; }
		cout << "전화번호: ";
		cin >> number;

		numberMap[name] = number;
	}
	cout << "<저장한 이름과 전화번호>" << endl;
	for (auto a = numberMap.begin(); a != numberMap.end(); ++a)
	{
		cout << a->first << " " << a->second << endl;
	}

	// 특정 이름에 대해서 전화번호를 출럭하는 프로그램
	cout << "\n검색할 이름 입력: ";
	string Name;
	cin >> Name;

	auto a = numberMap.find(Name); //find()로 이름 찾기

	if (a != numberMap.end()) { 
		cout << Name << "의 전화번호: " << a->second << endl;
	}
	else {
		cout << Name << "찾을 수 없습니다" << endl;
	}

}
```

