# pacman-multi-agent-search
- Q1: Reflex Agent
  + Đầu tiên là tìm khoảng cách từ vị trí hiện tại của pacman đến từng food, rồi chọn ra giá trị nhỏ nhất, gán vào biến minDistanceToFood.
  + Xét khoảng cách từ pacman đến các ghost, nếu < 2 thì trả về giá trị âm vô cùng (float("inf")) luôn.
  + Cuối cùng, trả về gía trị successorGameState.getScore() + 1.0/minDistanceToFood
  
- Q2: Minimax
  + Tạo thêm 3 hàm minimax, maxVal, và minVal đều có các tham số gameState, agentIndex, depth.
  + Hàm minimax trả về self.evaluationFunction(gameState) nếu depth = self.depth * gameState.getNumAgents() hoặc trạng thái game là đã thua, hoặc trạng thái game là đã thắng. Nếu không, hàm sẽ trả về hàm maxVal nếu angentIndex = 0, tức là pacman. Ngược lại, agentIndex != 0, tức là ghost, hàm sẽ trả về hàm minVal.
  + Hàm maxVal khởi tạo biến bestAction là 1 mảng gồm 2 phần tử, đầu tiên là action có giá trị là "max", còn lại là score có giá trị là âm vô cùng. Tiếp theo, xét danh sách legalActions, tìm ra succAction cũng gồm 2 phần tử như bestAction. Sau đó dựa trên việc so sánh phần tử score để lấy ra action có score lớn hơn. Cuối cùng trả về biến đó.
  + Hàm minVal tương tự maxVal, chỉ thay giá trị khởi tạo của phần tử score của bestAction = dương vô cùng. Và khi so sánh score thì chọn ra biến có score nhỏ hơn rồi trả về.
  + Hàm getAction chính, trả về maxVal()[0], tức là lấy phần tử đầu tiên (action) của giá trị trả về.
  
- Q3: Alpha-Beta Pruning
  + Cùng tạo thêm 3 hàm đó là maxVal, minVal, hàm alphabeta thay cho hàm minimax. Tương tự như câu 2, chỉ thêm 2 tham số alpha và beta vào 3 hàm trên.
  + Trong hàm maxVal, sau khi tìm ra action có score lớn hơn thì sẽ so sánh score đó với beta, nếu lớn hơn beta thì trả về action như bài 2, ngược lại gán alpha = giá trị lớn hơn giữa alpha và score rồi vẫn trả về action.
  + Trong hàm minVal, sau khi tìm ra action có score nhỏ hơn thì sẽ so sánh score đó với alpha, nếu nhỏ hơn alpha thì trả về action như bài 2, ngược lại gán beta = giá trị nhỏ hơn giữa beta và score rồi vẫn trả về action.
  
- Q4: Expectimax
  + Tương tụ bài 2, bài Minimax, chỉ thay đối hàm minVal.
  + Trong hàm minVal, khởi tạo biến totalScore = 0.
  + Xét danh sách legalActions, tìm bestAction như tìm succAction ở bài 2, cũng gồm 2 giá trị là action và score. Tính tổng các score và cập nhật vào biến totalScore.
  + Hàm minVal trả về action và trung bình score (totalScore/len(legalActions)).
- Q5: Evaluation Function
  + Tương tự câu 1, chỉ thêm 2 biến là numOfGhostNear và numOfGhostNotScare.
  + numOfGhostNear sẽ bằng số lượng ghost có khoảng cách tới pacman < 3, numOfGhostNotScare bằng số lượng ghost có scaredTime = 0.
  + Hàm trả về tổng của các biến nhưng có thêm một vài hệ số: 
  10.0 * currentGameState.getScore() + 5.0/minDistanceToFood + 1.0 * numOfGhostNear + 1.0/(numOfGhostNotScare + 0.01)
