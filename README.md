# Program: LAB Assignment 6 - Business Loyalty
# This program uses a constructor to simulate a customer with their
# purchase amount, number of purchases, and gift certificates. The
# makePurchase method will first check if the purchase amount is in the valid
# format, then it checks if the purchase amount is greater than or equal to $100
# and number of purchases is greater than or equal to 3 to issue a gift
# certificate amount of $10. Otherwise, a normal purchase is executed.

# Customer Class
class Customer :

    # Intended class constants ------------------------------------
    DEFAULT_PURCH_AMT = 0
    DEFAULT_NUM_PURCH = 0
    DEFAULT_GIFT_CERT = 0
    PURCH_BONUS_NUM = 3
    PURCH_BONUS_AMT = 100
    GIFT_CERT = 10

    # constructor method ------------------------------------
    def __init__(self, pAmt = DEFAULT_PURCH_AMT, \
                 numP = DEFAULT_NUM_PURCH,
                 gCert = DEFAULT_GIFT_CERT) :
        # Initializing defaults
        self.pAmt = self.DEFAULT_PURCH_AMT
        self.numP = self.DEFAULT_NUM_PURCH
        self.gCert = self.DEFAULT_GIFT_CERT

        self.set_purchaseAmount(pAmt)
        self.set_numPurchases(numP)
        self.set_giftCertAmount(gCert)

    # mutator ("set") methods -------------------------------
    # Sets the initial purchase amount
    # @param amount purchase amount
    def set_purchaseAmount(self, amount) :
        if amount < self.DEFAULT_PURCH_AMT :
            return False
        else :
            self.pAmt = amount
            return True

    # Sets the number of purchases for a customer
    # @param numPurchases number of purchases
    def set_numPurchases(self, numPurchases) :
        if numPurchases < self.DEFAULT_NUM_PURCH :
            return False
        else :
            self.numP = numPurchases
            return True

    # Sets the gift certificate amount
    # @param amount gift certificate amount
    def set_giftCertAmount(self, amount) :
        if amount < self.DEFAULT_GIFT_CERT :
            return False
        else :
            self.gCert = amount
            return True

    # accessor ("get") methods -------------------------------
    # Returns the total purchase amount
    # @return total amount purchased
    def get_purchaseAmount(self) :
        return self.pAmt

    # Returns the total number of purchases
    # @return number of purchases
    def get_numPurchases(self) :
        return self.numP

    # Returns the gift certificate amount
    # @return gift certificate amount
    def get_giftCertAmount(self) :
        return self.gCert

    # Returns customers information
    # @return string of customers information
    def to_string(self) :
        return ("Purchase amount: $" + str(self.pAmt) + "\n" + \
                "Number purchases: " + str(self.numP) + "\n" + \
                "Gift certificate amount: $" + str(self.gCert))

    # Initiates a purchase, checks if amount purchased and number of purchases
    # reaches threshold for a gift certificate
    # @return True for certificate and False for invalid and regular purchase
    def makePurchase(self, amount) :
        # Invalid negative inputs
        if amount < self.DEFAULT_PURCH_AMT :
            return False

        # Add purchase amount, increase purchase number count
        self.pAmt = self.pAmt + amount
        self.numP = self.numP + 1

        # Gives a certificate if both thresholds are met
        if (self.pAmt >= self.PURCH_BONUS_AMT and \
            self.numP >= self.PURCH_BONUS_NUM) :
            self.giftReached()
            self.pAmt = self.DEFAULT_PURCH_AMT
            self.numP = self.DEFAULT_NUM_PURCH
            return True

        return False

    # Gives a gift certificate, increasing the gift certificate amount by 10
    def giftReached(self) :
        self.gCert = self.gCert + self.GIFT_CERT

# ------------- CLIENT --------------------------------------------------

# Main function for using the Customer object to simulate a customer's
# purchase amount, number of purchases, and gift certificate
def main() :

    # Purchase constants
    NEGATIVE_PURCHASE_AMT = -4
    TOTAL_PURCHASES = 7
    NEGATIVE_PURCHASE_INDEX = 3
    PURCHASE_AMT_CHANGE = 20

    # Purchase number counter
    purchase_counter = 0
    make_purchase_amt = 15

    # Create a Customer object Cust_1 = Customer()
    print("Initializing Customer Purchase")
    customer_1 = Customer()
    print(customer_1.to_string())
    print("--------------------")

    # Executes purchases
    for purchase_index in range(TOTAL_PURCHASES) :
        purchase_counter = purchase_index + 1
        print("New Purchase " + str(purchase_counter))

        # Runs a negative purchase
        if purchase_index == NEGATIVE_PURCHASE_INDEX :
            if customer_1.makePurchase(NEGATIVE_PURCHASE_AMT) == False :
                print("Invalid purchase amount: $" + \
                    str(NEGATIVE_PURCHASE_AMT))

        # Runs positive purchases, if true certificate is awarded
        else :
            if customer_1.makePurchase(make_purchase_amt) :
                print("Hooray! You received a gift certificate.")
                print("Gift certificate value: $" + \
                    str(customer_1.get_giftCertAmount()))
            make_purchase_amt = make_purchase_amt + PURCHASE_AMT_CHANGE

        # Displays customers information
        print(customer_1.to_string())
        print("--------------------")

# Running main function
main()
