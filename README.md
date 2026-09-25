# datetime
import datetime

def calculate_age_and_deadlines():
    print("=" * 50)
    print("     Smart Age & Deadline Calculator Application 📅     ")
    print("=" * 50)
    
    # -------------------------------------------------------------------------
    # Part 1: Detailed Age Calculator (Years, Months, Days)
    # -------------------------------------------------------------------------
    print("\n[1] Detailed Age Calculator:")
    birth_input = input("Enter your birth date (DD-MM-YYYY) e.g., 15-08-1995: ")
    
    try:
        # Convert the string input into a date object using strptime
        birth_date = datetime.datetime.strptime(birth_input, "%d-%m-%Y").date()
        today = datetime.date.today()
        
        # Calculate total days lived
        total_days = (today - birth_date).days
        
        # Calculate broken-down age (years, months, days)
        years = today.year - birth_date.year
        months = today.month - birth_date.month
        days = today.day - birth_date.day
        
        # Adjust calculations if days or months turn out negative
        if days < 0:
            months -= 1
            # Fetch the total days of the previous month
            prev_month = today.month - 1 if today.month > 1 else 12
            prev_year = today.year if today.month > 1 else today.year - 1
            days += (datetime.date(today.year, today.month, 1) - datetime.date(prev_year, prev_month, 1)).days
            
        if months < 0:
            years -= 1
            months += 12
            
        print(f"\n🎉 Your current age is: {years} years, {months} months, and {days} days.")
        print(f"🔢 Total days you have lived up to today: {total_days:,} days.")
        
    except ValueError:
        print("❌ Invalid date format! Please enter the date exactly like (25-09-2000).")
        return

    # -------------------------------------------------------------------------
    # Part 2: Deadline Calculator (Visas, Residencies, Projects)
    # -------------------------------------------------------------------------
    print("\n" + "-" * 50)
    print("[2] Deadline / Expiry Calculator:")
    
    start_input = input("Enter start date (DD-MM-YYYY) or press Enter for TODAY: ")
    
    # Determine the starting point (Today or User Input)
    if start_input.strip() == "":
        start_date = datetime.date.today()
        print(f"-> Base date set to Today: {start_date.strftime('%d-%m-%Y')}")
    else:
        try:
            start_date = datetime.datetime.strptime(start_input, "%d-%m-%Y").date()
        except ValueError:
            print("❌ Invalid date format!")
            return
            
    days_to_add = input("Enter number of days to add (e.g., 130 or 180): ")
    
    try:
        days_count = int(days_to_add)
        # Use timedelta to accurately calculate the future date
        expiry_date = start_date + datetime.timedelta(days=days_count)
        
        # Format the result elegantly using strftime
        clear_expiry = expiry_date.strftime("%Y-%m-%d")
        day_name = expiry_date.strftime("%A")
        
        print(f"\n✅ Result:")
        print(f"The exact expiry date after {days_count} days is: {clear_expiry} ({day_name})")
        
    except ValueError:
        print("❌ Please enter a valid number of days (digits only).")

# Run the application
if __name__ == "__main__":
    calculate_age_and_deadlines()
