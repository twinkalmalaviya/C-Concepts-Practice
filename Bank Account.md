```C++
#include<iostream>
using namespace std;

class account
{

    double Ac_balance=0;
    string holder_name;

public:
    enum class TYPE : uint32_t
    {
        SAVING = 0,
        CURRENT
    };
    TYPE AC_TYPE;
    account(const string name) : holder_name{name}
    {
        
    }
    virtual ~account()
    {
        cout << holder_name<<" deleted"<<endl;
    }
    void deposit(double de_amount)
    {
        Ac_balance = Ac_balance + de_amount;
    }
    void withdraw(double Wd_amount)
    {
        if (Wd_amount <= Ac_balance)
            Ac_balance -= Wd_amount;
        else
        {
            
        }
        
    }
    TYPE type()
    {
        return AC_TYPE;
    }
    string holder()
    {
        return holder_name;

    }
    double balance()
    {
        return Ac_balance;
    }
    virtual float interest_rate()
    {
        return 0;
    }
};

class saving_account:public account
{
    float Int_rate;

public:
    saving_account(const string name, float rate = 4.5) : account(name), Int_rate(rate)
    {

        /* code */
        AC_TYPE = TYPE::SAVING;
    }
    ~saving_account()
    {
        cout << "saving account of ";
    }
    virtual float interest_rate()
    {
        return Int_rate;
    }
};

class current_account:public account
{
    float Int_rate;

public:
    current_account(const string name,float rate = 4.0) : account(name),Int_rate(rate)
    {
        AC_TYPE = TYPE::CURRENT;
    }
    ~current_account()
    {
        cout << "current_account of ";
    }
    virtual float interest_rate()
    {
        return Int_rate;
    }
};


double fixed_deposit_rate(account *ac)
{
    return (ac->type() == account::TYPE::SAVING) ? 6.5 : 4.0;
}

void delete_account(account *ac)
{
    delete ac;
}

void print_saving_account(account *ac)
{
   // if (/* type casting condition to print saving account only */) // Do not use ac->type() method
   if (ac->AC_TYPE == account::TYPE::SAVING)
   {
       cout << "holder : " << ac->holder() << endl;
       cout << "balance : " << ac->balance() << endl;
       cout << "interest rate : " << ac->interest_rate() << endl;
       cout << "FD rates : " << fixed_deposit_rate(ac) << endl;
    }
}

int main()
{
    saving_account *s_ac = new saving_account("John");
    s_ac->deposit(1000);
    s_ac->withdraw(100.30);
    print_saving_account(s_ac);
    delete_account(s_ac);
    cout << endl;

    current_account *c_ac = new current_account("Mathew");
    c_ac->deposit(10);
    c_ac->withdraw(100.30);
    print_saving_account(c_ac);
    delete_account(c_ac);
    cout << endl;

    return 0;
}
```
