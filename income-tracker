from datetime import datetime

# Get safe float input
def get_float(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Please enter a valid number.")

# Get optional input or default fallback
def get_input(prompt):
    value = input(prompt).strip()
    return value if value else "Not provided"

# Main app
def cash_kitten():
    print("\n🐾 Welcome to Cash Kitten — Track That Tip Money, Babe 🐾\n")

    session_name = input("Name this session (e.g. 'FridayShift' or 'ClubKitty_7-11'): ").strip()
    now = datetime.now()
    date_str = now.strftime("%Y-%m-%d %I:%M %p")

    entries = []
    while True:
        entry = input("💸 Enter an income amount (or type 'done' to finish): $").strip()
        if entry.lower() == "done":
            break
        try:
            earning = float(entry)
            time_input = input("⏰ What time was this? (e.g. 11:45 PM): ")
            entries.append((earning, time_input))
        except ValueError:
            print("Please enter a valid number or type 'done'.")

    if not entries:
        print("No earnings entered. Exiting.")
        return

    gross_total = sum(e[0] for e in entries)
    print(f"\nTotal earnings entered: ${gross_total:.2f}")

    # Deductions
    house_fee = get_float("🏠 Enter flat house fee: $")
    club_percent = get_float("🎯 Enter club's % cut (e.g. 20 for 20%): ")
    club_cut = (club_percent / 100) * gross_total

    extra_deductions = []
    while True:
        label = input("➕ Enter a label for a one-time deduction (or press Enter to skip): ")
        if not label:
            break
        amount_prompt = f'   💸 How much was "{label}"?: $'
        amount = get_float(amount_prompt)
        extra_deductions.append((label, amount))

    total_deductions = house_fee + club_cut + sum(d[1] for d in extra_deductions)
    net_income = gross_total - total_deductions

    # Savings
    save_choice = input("🐖 Would you like to set aside money for savings today? (yes/no): ").lower()
    savings_amount = 0
    savings_goal = ""
    if save_choice == "yes":
        save_type = input("   Enter 'percent' or 'flat': ").lower()
        if save_type == "percent":
            save_percent = get_float("   What % of your net income would you like to save?: ")
            savings_amount = (save_percent / 100) * net_income
        else:
            savings_amount = get_float("   How much to save?: $")
        savings_goal = input("   Optional savings goal name (e.g. 'Rent', 'Vacation'): ")

    remaining_after_savings = net_income - savings_amount

    # Budget breakdown
    rent = 0.40 * net_income
    food = 0.20 * net_income
    savings = 0.20 * net_income
    other = 0.20 * net_income

    # Notes
    mood = get_input("💅 Mood today: ")
    outfit = get_input("👗 What did you wear?: ")
    notes = get_input("📝 Extra notes (clients, convos, etc.): ")

    # Save log file
    filename = f"{session_name}_{now.strftime('%Y%m%d_%H%M%S')}.txt"
    with open(filename, "w") as file:
        file.write(f"🐾 Cash Kitten — {session_name} 🐾\n")
        file.write(f"Date: {date_str}\n\n")
        file.write("💸 Income Entries:\n")
        for amount, time in entries:
            file.write(f" - ${amount:.2f} at {time}\n")
        file.write(f"\n🏠 House Fee: ${house_fee:.2f}")
        file.write(f"\n🎯 Club Cut ({club_percent}%): ${club_cut:.2f}")
        for label, amount in extra_deductions:
            file.write(f"\n➕ {label}: ${amount:.2f}")
        file.write(f"\n\nTotal Deductions: ${total_deductions:.2f}")
        file.write(f"\nNet Income: ${net_income:.2f}")
        if save_choice == "yes":
            file.write(f"\n🐖 Saved: ${savings_amount:.2f} → Goal: {savings_goal}")
            file.write(f"\nRemaining After Savings: ${remaining_after_savings:.2f}")
        file.write("\n\n📊 Budget Breakdown:")
        file.write(f"\n - Rent (40%): ${rent:.2f}")
        file.write(f"\n - Food (20%): ${food:.2f}")
        file.write(f"\n - Savings (20%): ${savings:.2f}")
        file.write(f"\n - Other (20%): ${other:.2f}")
        file.write("\n\n📝 Notes:")
        file.write(f"\n - Mood: {mood}")
        file.write(f"\n - Outfit: {outfit}")
        file.write(f"\n - Extra: {notes}")

    print(f"\n✅ Log saved as: {filename}")
    print("Thanks for tracking like a boss. 💖")

# Run it
cash_kitten()
