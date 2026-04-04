---
title: "Usage"
description: "Usage guide for foltone_drivingschool script"
script: "foltone-drivingschool"
section: "Driving School"
order: 3
version: "1.0.0"
---

# Usage

## Accessing the driving school

1. Go to the driving school location marked on the map.
2. Approach the instructor NPC.
3. Press the interaction key to open the menu.

## Theory exam (road code)

### How it works

1. Select "Theory Exam" from the menu.
2. Pay the registration fee.
3. A NUI interface appears with the questions.
4. For each question:
   - Read the question and proposed answers.
   - Click on your chosen answer.
   - A timer is displayed (time limit per question).
5. At the end of the exam, your score is displayed.

### Result

- **Pass** (score >= configured threshold): You can proceed to practical exams.
- **Fail**: You must pay again and retake the exam.

## Practical exams

Three types of practical exams are available:

### Car exam

1. Select "Car Exam" from the menu.
2. Pay the fee.
3. An exam vehicle spawns.
4. Get in the vehicle and follow the route (checkpoints).
5. Follow the rules:
   - Do not exceed the speed limit.
   - Avoid collisions.
   - Pass through all checkpoints in order.
6. At the end of the route, the result is announced.

### Motorcycle exam

Same principle as the car exam, with a two-wheeled vehicle and a dedicated route.

### Truck exam

Same principle, with a truck and a lower error tolerance.

## License granting

On passing:

| Exam | License granted |
|---|---|
| Car | `drive` |
| Motorcycle | `drive_bike` |
| Truck | `drive_truck` |

The license is automatically added via esx_license and is permanent.

## Failure

On failing a practical exam:

- The exam vehicle is deleted.
- You must pay the fee again to retry.
- No cooldown is imposed (unless configured).

## Tips

- Review questions before taking the theory exam.
- Drive carefully during practical exams.
- Watch out for pedestrians: hitting a pedestrian causes immediate failure.
