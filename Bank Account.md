```c++
#include<iostream>

class account
{
    std::string name;
    double ac_balance;
    
public:
    enum TYPE
    {
        SAVING = 0,
        CURRENT
    } ;
    TYPE Ac_type;
    account(std::string h_name, TYPE type,double op_bal = 0) : name{h_name}, ac_balance{op_bal}, Ac_type{type}
    {

    }
    virtual ~account(){
        std::cout << " " << name <<" deleted\n ";
    } std::string holder()
    {
        return name;
    }
    double balance()
    {
        return ac_balance;
    }

     void deposit(double de_amount)
    {
        ac_balance = ac_balance + de_amount;
    }
     void withdraw(double Wd_amount)
    {
        if (Wd_amount <= ac_balance)
            ac_balance -= Wd_amount;
        else
        {
            std::cout<<"ac_balance is less then withdrawl amout\n";
        }
    }
    TYPE type()
    {
        return Ac_type;
    }
    virtual double interest_rate()=0;
};

class saving_account:public account
{
    double in_rate;
public:
    saving_account(std::string name,double op_bal=0,double ist_rate=4.5):account(name,TYPE::SAVING,op_bal)
    {
        in_rate =ist_rate;
    }
    ~saving_account()
    {
        std::cout << "saving account of";
    }
    double interest_rate()
    {
        return in_rate;
    }
};

class current_account:public account
{
    double in_rate;
public:
    current_account(std::string name, double op_bal = 0, double ist_rate = 4) : account(name,TYPE::CURRENT, op_bal)
    {
        in_rate = ist_rate;
    }
    ~current_account()
    {
        std::cout << "current account of";
    }
    double interest_rate()
    {
        return in_rate;
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
    if (dynamic_cast<saving_account *>(ac))
    {
        std::cout << "holder : " << ac->holder() << std::endl;
        std::cout << "balance : " << ac->balance() << std::endl;
        std::cout << "interest rate : " << ac->interest_rate() << std::endl;
        std::cout << "FD rates : " << fixed_deposit_rate(ac) << std::endl;
    }
}

int main()
{
    saving_account *s_ac = new saving_account("John");
    s_ac->deposit(1000);
    s_ac->withdraw(100.30);
    print_saving_account(s_ac);
    delete_account(s_ac);
    std::cout << std::endl;

    current_account *c_ac = new current_account("Mathew");
    c_ac->deposit(10);
    c_ac->withdraw(100.30);
    print_saving_account(c_ac);
    delete_account(c_ac);
    std::cout << std::endl;

    return 0;
}
```
