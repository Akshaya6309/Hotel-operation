# Hotel-operation
#	This project is a Python-based application that simulates basic banking operations. It allows users to login,  and see menu, add to cart for order, payment. 
#	Languages Used: - Python.

class hotel:
    r_name='behrouz'
    r_address='hyd'
    cust_details={}
    cart_details={}
    def __init__(self,name,phone_no,gender,email,password,pin):
        self.name=name
        self.phone=phone_no
        self.gender=gender
        self.email=email
        self.password=password
        self.pin=pin
        self.concat_cust_details(self.name,self)

    @classmethod
    def concat_cust_details(cls,name,self):
        cls.cust_details[name]=self       

    @classmethod
    def login(cls):
        name=input('enter ur name')
        password=int(input('enter ur pswd'))
        if name in cls.cust_details and password==cls.cust_details[name].password:
            print("login successfull")
            cls.main_menu(name)
        else:
            print("incorrect pwsd")
    @classmethod
    def main_menu(cls,name):
        n=int(input('choose 1.Veg\n 2.Non_veg\n 3.Desserts\n 4.Cooldrinks \n5.check order_details'))
        match n:
            case 1:
                cls.veg(name)
            case 2:
                cls.non_veg(name)
            case 3:
                cls.desserts(name)
            case 4:
                cls.cooldrinks(name)
            case 5:
                cls.order_details(name)
            case _:
                return
        return    
    @classmethod
    def veg(cls,name):
        n=int(input('choose 1.Veg starters\n 2.main_course\n 3.back to main menu 4.exit'))
        match n:
            case 1:
                print("SNO Dish Price")
                print("________________")
                print('1.paneerTikka: 230')
                print('2.manchuriya - price : 120')
                print('3.curry - price : 150')
                print('4.mushroom - price : 250')
                cls.veg_starters(name)
            case 2:
                print('1.Veg Biryani - price : 150')
                print('2.paneerBiryani - price : 200')
                print('3.VegThali - price : 180')
                print('4.chapati with paneercurry - price : 200')
                cls.main_course(name)
            case 3:
                cls.main_menu(name)
            case _:
                return
        # cls.veg(name)    
    @classmethod
    def veg_starters(cls,name):
        m=int(input('choose'))
        match m:
            case 1:
                q=int(input("enter quantity"))
                cls.add_cart(name,'paneertikka',q)
            case 2:
                q=int(input("enter quantity"))
                cls.add_cart(name,'manchuriya',q)
            case 3:
                q=int(input("enter quantity"))
                cls.add_cart(name,'curry',q)
            case 4:
                q=int(input("enter quantity"))
                cls.add_cart(name,'mushroom',q)

            case _:
                return
            
    @classmethod
    def add_cart(cls,self,dish='',q=1):
        d={'paneertikka': 230,'manchuriya': 120,'curry': 150,'mushroom': 250,'Veg Biryani': 150,'paneerBiryani': 200,'VegThali': 180,'chapati with paneercurry': 200,'chickenTikka': 230,'Fishfry': 320,'chicken65': 250,'chilli chicken': 250,'chicken Biryani': 350,'muttonBiryani': 200,'chickenmandi': 380,'chapati with butterchicken': 300,'ice cream':100,'sweets':120,'gulabjam':50,'fruitsalad':100,'coco cola':50,'sprite':50,'thumpsup':50,'mango juice':50}
        
        cls.cart(self,{'dish':dish,'quantity':q,'price':d[dish]*q})
                
    @classmethod
    def cart(cls,self,items):
        if self not in cls.cart:
            cls.cart_details[self]=[items]
        else:
            cls.cart_details[self]+=[items]


    @classmethod
    def order_details(cls,name):
        t_price=0
        for i in cls.cart_details[name]:
            print(i['dish'],i['quantity',i['price']])
            t_price+=i['price']
        print("total amount",t_price)
        res=cls.pay(name)
        if res=='success':
            print("order placed")
            # if name not in cls.cart:
            #     cls.order_history[name]=cls.cart
            # else:
            #     cls.order_history[name]+=cls.cart

    
