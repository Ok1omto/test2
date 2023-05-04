��#� �t�e�s�t�2�
�
�#include <iostream>
#include <algorithm>
#include <vector>
#include <Windows.h>

using namespace std;
HANDLE hConsole;

//создание класса 
class Spell {
public:
	int power_spell;
	int mana;
	Spell(int p, int m) {
		power_spell = p;
		mana = m;
	}

	//создание перегрузки оператора сравнения так, чтобы при сравнении двух объектов меньшим считался
	//тот, у которого расходуемая энергия меньше.
	bool operator<(const Spell& second) {
		if (this->mana == second.mana) {
			return this->power_spell > second.power_spell;
		}
		else {
			this->mana > second.mana;
		}
		return this->mana > second.mana;	
	}
};


//создание компаратора, который считает меньшим объект, у которого “сила заклинания” меньше.
bool comp(const Spell& first, const Spell& second) {
	return first.power_spell > second.power_spell;
}


int main() {
	setlocale(LC_ALL, "ru");
	hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
	//создание массива из векторов
	vector<Spell> v;
	v.push_back(Spell(15, 20));
	v.push_back(Spell(10, 19));
	v.push_back(Spell(25, 98));
	v.push_back(Spell(11, 15));
	v.push_back(Spell(2, 7));
	v.push_back(Spell(90, 178));
	//сортировка через оператор
	sort(v.begin(), v.end());
	SetConsoleTextAttribute(hConsole, 12);
	for (auto& b : v) {
		cout << "Мана: " << b.mana << " " << "Сила заклинания: " << b.power_spell << endl;
	}
	

	//сортировка через компаратор
	sort(v.begin(), v.end(), comp);
	SetConsoleTextAttribute(hConsole, 11);
	for (auto& b : v) {
		cout << "Сила заклинания: " << b.power_spell << " " << "Мана: " << b.mana << endl;
	}
}
