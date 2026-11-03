
import random

def play_game():
    secret_number = random.randint(1, 100)
    max_attempts = 5
    attempts = 0

    print("\n===== بازی حدس اعداد =====")
    print("یک عدد بین 1 تا 100 حدس بزن.")
    print("برای بردن بازی 5 فرصت داری.\n")

    while attempts < max_attempts:

        remaining = max_attempts - attempts

        print(f"تلاش {attempts + 1} از {max_attempts}")
        print(f"جان باقی‌مانده: {remaining}")

        user_input = input("حدس خود را وارد کن: ")

        # اعتبارسنجی ورودی
        try:
            guess = int(user_input)
        except ValueError:
            print("خطا! لطفاً فقط عدد وارد کن.\n")
            continue

        if guess < 1 or guess > 100:
            print("خطا! عدد باید بین 1 تا 100 باشد.\n")
            continue

        # ثبت تلاش معتبر
        attempts += 1

        # بررسی حدس
        if guess == secret_number:
            print("\nتبریک! عدد را درست حدس زدی.")

            # تعیین رتبه
            ranks = {
                1: "نمونه‌ای",
                2: "بسیار خوبی",
                3: "خوب",
                4: "قبول",
                5: "با شانس بردی!"
            }

            print(f"تعداد تلاش‌ها: {attempts}")
            print(f"رتبه شما: {ranks[attempts]}")
            break

        # تعیین جهت و اختلاف
        difference = abs(guess - secret_number)

        if guess < secret_number:
            direction = "بزرگ‌تر وارد کن!"
        else:
            direction = "کوچک‌تر وارد کن!"

        # راهنمای نزدیک یا دور
        if difference <= 5:
            distance_hint = "خیلی نزدیکی!"
        elif difference <= 15:
            distance_hint = "نزدیکی، ولی هنوز فاصله داری!"
        else:
            distance_hint = "خیلی دوری!"

        print(direction)
        print(distance_hint)
        print()

    else:
        # در صورت تمام شدن فرصت‌ها
        print("\nمتأسفانه باختی!")
        print(f"عدد مخفی {secret_number} بود.")

def main():
    while True:
        play_game()

        print("\nآیا می‌خواهی دوباره بازی کنی؟")
        answer = input("بله یا خیر (y/n): ").strip().lower()

        while answer not in ["y", "n", "yes", "no"]:
            answer = input("لطفاً y یا n وارد کن: ").strip().lower()

        if answer in ["n", "no"]:
            print("\nممنون از بازی کردن! خداحافظ.")
            break

main()
