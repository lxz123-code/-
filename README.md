#ifndef ELEPHANT_H
#define ELEPHANT_H
#include <string>
using namespace std;
// 大象类：封装“进入冰箱”功能
class Elephant {
private:
	string name; // 大象名字（增加个性化）
	bool isInFridge; // 是否在冰箱内
public:
	Elephant(string name); // 构造函数：初始化大象名字和状态
	void enterFridge(); // 进入冰箱函数
	bool getInFridgeStatus() const; // 获取是否在冰箱内（用于验证）
};
#endif

#ifndef REFRIGERATOR_H // 防止头文件重复包含
#define REFRIGERATOR_H
#include <string>
using namespace std;
// 冰箱类：封装“开门/关门”功能
class Refrigerator {
private:
	string status; // 冰箱状态："closed"（关闭）或 "open"（打开）
public:
	Refrigerator(); // 构造函数：初始化冰箱为关闭状态
	void openDoor(); // 开门函数
	void closeDoor(); // 关门函数
	string getStatus() const; // 获取当前状态（用于验证）
};
#endif

#include "Elephant.h"
#include <iostream>
using namespace std;
// 构造函数：初始化名字，初始不在冰箱内
Elephant::Elephant(string name) : name(name), isInFridge(false) {}
// 进入冰箱：仅当冰箱打开时可成功
void Elephant::enterFridge() {
	if (!isInFridge) {
		isInFridge = true;
		cout << name << "成功钻进冰箱啦！" << endl;
	}
	else {
		cout << name << "已经在冰箱里了，别挤啦~" << endl;
	}
}

// 获取是否在冰箱内
bool Elephant::getInFridgeStatus() const {
	return isInFridge;
}

#include "Refrigerator.h"
#include <iostream>
using namespace std;
// 构造函数：初始状态为“关闭”
Refrigerator::Refrigerator() : status("closed") {}
// 开门：仅当关闭时可操作
void Refrigerator::openDoor() {
	if (status == "closed") {
		status = "open";
		cout << "冰箱门已打开！" << endl;
	}
	else {
		cout << "冰箱门本来就是开的，无需重复操作~" << endl;
	}
}

// 关门：仅当打开时可操作
void Refrigerator::closeDoor() {
	if (status == "open") {
		status = "closed";
		cout << "冰箱门已关闭！" << endl;
	}
	else {
		cout << "冰箱门本来就是关的，无需重复操作~" << endl;
	}
}

// 获取当前状态
string Refrigerator::getStatus() const {
	return status;
}

#include "Refrigerator.h"
#include "Elephant.h"
#include <iostream>
using namespace std;

int main() {
	// 1. 创建冰箱和大象对象
	Refrigerator myFridge;
	Elephant myElephant("壮壮");

	// 2. 执行“装大象”流程
	cout << "===== 开始装大象 =====" << endl;
	myFridge.openDoor();       // 第一步：开冰箱门
	myElephant.enterFridge();  // 第二步：大象进冰箱
	myFridge.closeDoor();      // 第三步：关冰箱门

	// 3. 验证结果
	cout << "\n===== 结果验证 =====" << endl;
	cout << "冰箱当前状态：" << myFridge.getStatus() << endl;
	cout << "大象是否在冰箱内：" << (myElephant.getInFridgeStatus() ? "是" : "否") << endl;

	return 0;
}
