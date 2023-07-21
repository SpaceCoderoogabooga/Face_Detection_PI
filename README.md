# Face_Detection_PI
import cv2
import numpy as np

face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')
cap = cv2.VideoCapture(0)

def single_out_face(faces):

    biggest_face = [0, 0, 0, 0]
    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x + w, y + h), (255, 0, 0), 2)
        if w > biggest_face[2]:
            biggest_face = [x, y, w, h]
    return biggest_face



while True:
    ret, frame = cap.read()
    if ret:
        cv2.imwrite("frame.jpg", frame)
        gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
        dimensions = frame.shape
        print(dimensions)
        faces = face_cascade.detectMultiScale(gray, 1.1, 4)
        target = single_out_face(faces)
        print(target)

        x, y, w, h = target
        left_bottom_corner = x, y
        left_upper_corner = x, (y + h)
        right_bottom_corner = (x + w), y
        right_upper_corner = (x + w), (y + h)
        left_center = x, y + int(h/2)
        right_center = (x + w), y + int(h/2)
        upper_center = (x + int(w/2)), (y + h)
        bottom_center = (x + int(w/2)), y
        target_center = (x + int(w/2)), (y + int(h/2))

        x0, y0 = 240, 320
        x999, y999 = 240, 320
        x1, y1 = 310, 240
        x2, y2 = 330, 240
        x3, y3 = 320, 235
        x4, y4 = 320, 245

        x5, y5 = 320, 220
        x6, y6 = 320, 190

        x7, y7 = 320, 260
        x8, y8 = 320, 290

        x9, y9 = 290, 240
        x10, y10 = 260, 240

        x11, y11 = 350, 240
        x12, y12 = 380, 240

        x13, y13 = 390, 230
        x14, y14 = 390, 190

        x15, y15 = 390, 250
        x16, y16 = 390, 290

        x17, y17 = 250, 250
        x18, y18 = 250, 290

        x19, y19 = 250, 190
        x20, y20 = 250, 230

        x21, y21 = 250, 190
        x22, y22 = 290, 190

        x23, y23 = 250, 190
        x24, y24 = 250, 290

        x25, y25 = 250, 190
        x26, y26 = 250, 290

        x27, y27 = 250, 190
        x28, y28 = 250, 230



        line_thickness = 1
        cv2.line(frame, (x3, y3), (x4, y4), (255, 255, 255), thickness=line_thickness)
        cv2.line(frame, (x1, y1), (x2, y2), (255, 255, 255), thickness=line_thickness)

        cv2.line(frame, (x5, y5), (x6, y6), (255, 255, 255), thickness=line_thickness)
        cv2.line(frame, (x7, y7), (x8, y8), (255, 255, 255), thickness=line_thickness)
        cv2.line(frame, (x9, y9), (x10, y10), (255, 255, 255), thickness=line_thickness)
        cv2.line(frame, (x11, y11), (x12, y12), (255, 255, 255), thickness=line_thickness)

        cv2.line(frame, (x0, y0), (x999, y999), (43, 255, 0), thickness=line_thickness)

        point1 = (320, 240)
        point2 = target_center
        point1_np = np.array(point1)
        point2_np = np.array(point2)
        distance = np.linalg.norm(point1_np - point2_np)
        print("                                                                                     ╔══════╗")
        print("                                                                             Distance: ", distance)
        print("                                                                                     ╚══════╝")

        width, height = 480, 640
        font = cv2.FONT_HERSHEY_SIMPLEX
        font_scale = 2
        thickness = 2

        position = (10, 100)
        color = (11, 198, 11)  # White color (BGR format)

        number = int(distance)
        cv2.putText(frame, str(number), position, font, font_scale, color, thickness, cv2.LINE_AA)


        # cv2.line(frame, (x13, y13), (x14, y14), (43, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x15, y15), (x16, y16), (43, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x17, y17), (x18, y18), (43, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x19, y19), (x20, y20), (43, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x21, y21), (x22, y22), (43, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x23, y23), (x24, y24), (43, 255, 0), thickness=line_thickness)














        # print(left_bottom_corner)
        # print(left_upper_corner)
        # print(right_bottom_corner)
        # print(right_upper_corner)









        # width, height = 800, 600
        # x1, y1 = 300, 240
        # x2, y2 = 340, 240
        # x3, y3 = 320, 220
        # x4, y4 = 320, 260
        # x5, y5 = 320, 240

        if distance < 400:
            line_thickness = 1
            cv2.line(frame, left_center, right_center, (0, 0, 255), thickness=line_thickness)
            cv2.line(frame, bottom_center, upper_center, (0, 0, 255), thickness=line_thickness)
            cv2.line(frame, target_center, (320, 240), (255, 255, 0), line_thickness)
            print("                                             - MOVEMENT -")

            if distance < 350:
                line_thickness = 1
                cv2.line(frame, left_center, right_center, (0, 0, 255), thickness=line_thickness)
                cv2.line(frame, bottom_center, upper_center, (0, 0, 255), thickness=line_thickness)
                cv2.line(frame, target_center, (320, 240), (0, 255, 255), line_thickness)
                print("                                            0- ALERT -0")
                if distance < 300:
                    line_thickness = 1
                    cv2.line(frame, left_center, right_center, (0, 0, 255), thickness=line_thickness)
                    cv2.line(frame, bottom_center, upper_center, (0, 0, 255), thickness=line_thickness)
                    cv2.line(frame, target_center, (320, 240), (255, 255, 255), line_thickness)


                    if distance < 250:
                        cv2.line(frame, target_center, (320, 240), (0, 128, 255), line_thickness)
                        print("                                            READY")






                    if distance < 200:
                        line_thickness = 1
                        cv2.line(frame, target_center, (320, 240), (0, 0, 255), line_thickness)
                        print("                                            ▐░░░░░░ LOCKED ░░░░░░░▌")
                        if distance < 100:
                            line_thickness = 1
                            cv2.line(frame, target_center, (320, 240), (0, 0, 255), line_thickness)
                            print("                                                                                            █ ✪ █▓▓▓▓ LOCKED ▓▓▓▓▓█ ✪ █   ")
                            if distance < 50:
                                line_thickness = 1
                                cv2.line(frame, target_center, (320, 240), (0, 0, 255), line_thickness)








        # cv2.line(frame, (x5, y5), (0, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x3, y3), (x4, y4), (0, 255, 0), thickness=line_thickness)
        # cv2.line(frame, (x1, y1), (x2, y2), (0, 255, 0), thickness=line_thickness)
        # start_point = x5, y5
        # end_point = x6, y6

        cv2.imshow(winname='frame', mat=frame)
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
cv2.imshow("Number Image", frame)

cap.release()
cv2.destroyAllWindows()
