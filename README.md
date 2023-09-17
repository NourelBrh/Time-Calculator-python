# Time-Calculator-python
def add_time(start_time, duration, start_day=None):
    # Parse the start time
    start_time_parts = start_time.split()
    time_parts = start_time_parts[0].split(':')
    hours, minutes = int(time_parts[0]), int(time_parts[1])
    am_pm = start_time_parts[1]

    # Parse the duration
    duration_parts = duration.split(':')
    duration_hours, duration_minutes = int(duration_parts[0]), int(duration_parts[1])

    # Convert AM/PM to 24-hour format
    if am_pm == 'PM':
        hours += 12

    # Calculate the total minutes
    total_minutes = hours * 60 + minutes + duration_hours * 60 + duration_minutes

    # Calculate the new time and days later
    new_hours, new_minutes = divmod(total_minutes, 60)
    days_later = new_hours // 24
    new_hours = new_hours % 24

    # Determine AM/PM
    if new_hours >= 12:
        am_pm = 'PM'
        if new_hours > 12:
            new_hours -= 12
    else:
        am_pm = 'AM'
        if new_hours == 0:
            new_hours = 12

    # Determine the day of the week
    days_of_week = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
    if start_day:
        start_day = start_day.lower().capitalize()
        start_index = days_of_week.index(start_day)
        new_day_index = (start_index + days_later) % 7
        new_day = days_of_week[new_day_index]

    # Construct the result string
    result = f"{new_hours:02}:{new_minutes:02} {am_pm}"
    if start_day:
        result += f", {new_day}"

    if days_later == 1:
        result += " (next day)"
    elif days_later > 1:
        result += f" ({days_later} days later)"

    return result
