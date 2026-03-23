# Lab-7-OOP-labs-PRACTICE-LAB-
## Joshua Vega solis 3-22-2026
##Extending Stack class behavior


```python
class Stack:
    def __init__(self):
        self.__stk = []

    def push(self, val):
        self.__stk.append(val)

    def pop(self):
        val = self.__stk[-1]
        del self.__stk[-1]
        return val


class CountingStack(Stack):
    def __init__(self):
        Stack.__init__(self)
        # Hidden property to count pops
        self.__counter = 0

    def get_counter(self):
        return self.__counter

    def pop(self):
        # Call the parent pop and increase counter
        val = Stack.pop(self)
        self.__counter += 1
        return val


stk = CountingStack()
for i in range(100):
    stk.push(i)
    stk.pop()
print(stk.get_counter())
```


##Implementing a queue class from scratch


```python
class QueueError(IndexError):
    pass


class Queue:
    def __init__(self):
        self.__items = []

    def put(self, elem):
        # Insert at the beginning of the list
        self.__items.insert(0, elem)

    def get(self):
        if len(self.__items) == 0:
            raise QueueError
        # Remove from the end
        val = self.__items[-1]
        del self.__items[-1]
        return val


que = Queue()
que.put(1)
que.put("dog")
que.put(False)
try:
    for i in range(4):
        print(que.get())
except:
    print("Queue error")

   
```
###Extending a Queue class

```python
class QueueError(IndexError):
    pass


class Queue:
    def __init__(self):
        self.__items = []

    def put(self, elem):
        self.__items.insert(0, elem)

    def get(self):
        if len(self.__items) == 0:
            raise QueueError
        val = self.__items[-1]
        del self.__items[-1]
        return val


class SuperQueue(Queue):
    def isempty(self):
        # Check if the list inside Queue is empty
        # We can use the length of the list
        # Note: Since __items is private in Queue, 
        # normally we'd need a way to access it or make it protected.
        # For this exercise, I'm assuming it's accessible or using simple logic.
        return len(self._Queue__items) == 0


que = SuperQueue()
que.put(1)
que.put("dog")
que.put(False)
for i in range(4):
    if not que.isempty():
        print(que.get())
    else:
        print("Queue empty")
```

##Timer class

```python
def format_time(h, m, s):
    # Function to add leading zeros
    return f"{h:02}:{m:02}:{s:02}"

class Timer:
    def __init__(self, hours=0, minutes=0, seconds=0):
        self.__hours = hours
        self.__minutes = minutes
        self.__seconds = seconds

    def __str__(self):
        return format_time(self.__hours, self.__minutes, self.__seconds)

    def next_second(self):
        self.__seconds += 1
        if self.__seconds > 59:
            self.__seconds = 0
            self.__minutes += 1
            if self.__minutes > 59:
                self.__minutes = 0
                self.__hours += 1
                if self.__hours > 23:
                    self.__hours = 0

    def prev_second(self):
        self.__seconds -= 1
        if self.__seconds < 0:
            self.__seconds = 59
            self.__minutes -= 1
            if self.__minutes < 0:
                self.__minutes = 59
                self.__hours -= 1
                if self.__hours < 0:
                    self.__hours = 23


timer = Timer(23, 59, 59)
print(timer)
timer.next_second()
print(timer)
timer.prev_second()
print(timer)
```

##Weeker class
```python

class WeekDayError(Exception):
    pass


class Weeker:
    __days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']

    def __init__(self, day):
        if day not in self.__days:
            raise WeekDayError
        self.__current = day

    def __str__(self):
        return self.__current

    def add_days(self, n):
        idx = self.__days.index(self.__current)
        new_idx = (idx + n) % 7
        self.__current = self.__days[new_idx]

    def subtract_days(self, n):
        idx = self.__days.index(self.__current)
        new_idx = (idx - n) % 7
        self.__current = self.__days[new_idx]


try:
    weekday = Weeker('Mon')
    print(weekday)
    weekday.add_days(15)
    print(weekday)
    weekday.subtract_days(23)
    print(weekday)
    weekday = Weeker('Monday')
except WeekDayError:
    print("Sorry, I can't serve your request.")
```


    ChallengueS
The most difficult part for me was understanding how private variables work with the double underscores because I kept getting errors when trying to use them in the new classes. I also struggled a bit with the inheritance part, specifically remembering to call the parent constructor so the list would work correctly. The logic for the Timer and the Weeker was also a challenge because I had to make sure the numbers and days would reset to zero or start over after reaching the limit. It took me a few tries to get the if statements and the calculations right.

