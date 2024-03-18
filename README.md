# Laba-5-OOP
Пример односвязного списка 
using namespace std;
#include <iostream> // для cout
#include <iomanip> // Для setw - Устанавливает фиксированную ширину

struct Laba5 { bool State; enum Motor {Diesel, Reactive, Electric}; 
Motor Name; int Index; Laba5* next = nullptr; }; 

const char *MotorName[] {"Дизельный", "Реактивный", "Электрический"}; 
const char *StateName[] {"Включено", "Выключено"};

void fVivoda(Laba5* first)
{ Laba5* current = first;
  while (current != nullptr)
{cout<< "Двигатель: "<< setw(13) << MotorName[current->Name] << "-" << current->Index << setw(19) << "Состояние: " << StateName[current->State] << endl;
current = current->next; } }

void fDelete(Laba5* first)
{ Laba5* current = first;
while (current != nullptr) 
{Laba5 *temp = current ;
current = current->next;
delete temp; }}

void fProcessData(Laba5* first) 
{int DieselCount=0;
  int jetCount=0;
  int electricCount=0;
  Laba5* current = first;
  while (current != nullptr)
{if (current->State)
{switch (current->Name)
	{case Laba5::Diesel:	DieselCount++;	break;
	case Laba5::Reactive:	jetCount++;		break;
	case Laba5::Electric:	electricCount++;	break; } } 
	current = current->next; }
cout << "Включенных Дизельных двигателей: " << DieselCount << endl;
cout << "Включенных Реактивных двигателей: " << jetCount << endl;
cout << "Включенных Электрических двигателей: " << electricCount << endl;}

void fAddInEnd(Laba5*& first, bool State, Laba5::Motor Name, int& IndexDiesel, int& IndexReactive, int& IndexElectric)
{ if (first == nullptr) { first = new Laba5 {State, Name, 0, nullptr}; }
  else { Laba5* current = first;
	  while (current->next != nullptr) {current = current->next;}
switch (Name) 
{ case Laba5::Diesel: current->Index = ++IndexDiesel;	break;
   case Laba5::Reactive: current->Index = ++IndexReactive;	break;
   case Laba5::Electric: current->Index = ++IndexElectric;	break; } 
   current->next = new Laba5{State,Name, current->Index+1, nullptr}; }}

int main()
{setlocale(LC_ALL, "ru");
Laba5* first = nullptr;
int IndexDiesel=0, IndexReactive=0, IndexElectric=0, Index = 0;
for (int i = 0; i < 10; i++) { bool State = (i % 2 == 0);
Laba5::Motor Name = static_cast<Laba5::Motor>(i % 3);
fAddInEnd(first, State, Name, IndexDiesel, IndexReactive, IndexElectric); }
fVivoda(first);	cout << endl;	fProcessData(first);	fDelete(first);
return 0;}
