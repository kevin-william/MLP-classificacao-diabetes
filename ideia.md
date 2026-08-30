um modelo MLP simples usando pytorch.

o modelo será um modelo de classificação e usará o dataset "C:\\workspace\\python\\mlp-classificacao\\dataset\\diabetes\_prediction\_dataset.csv"



vamos usar uma classe flexível para nosso modelo MLP como no exemplo: 



class MLP(nn.Module):

&#x20;   def \_\_init\_\_(self, in\_dim, hidden\_dims, num\_classes, dropout=0.0):

&#x20;       super().\_\_init\_\_()

&#x20;       layers = \[]

&#x20;       prev = in\_dim

&#x20;       for h in hidden\_dims:                         

&#x20;           layers.append(nn.Linear(prev, h))

&#x20;           layers.append(nn.BatchNorm1d(h))

&#x20;           layers.append(nn.ReLU())

&#x20;           layers.append(nn.Dropout(dropout))

&#x20;           prev = h

&#x20;       layers.append(nn.Linear(prev, num\_classes))   # cabeça final

&#x20;       self.net = nn.Sequential(\*layers)



&#x20;   def forward(self, x):

&#x20;       return self.net(x)



com uma função de treino como no exemplo:

def treinar(model, train\_loader, val\_loader, criterion, optimizer, epochs=50):

&#x20;   history = {'train\_loss': \[], 'val\_loss': \[], 'val\_acc': \[]}  

&#x20;   for epoch in range(epochs):

&#x20;       model.train()

&#x20;       train\_loss = 0

&#x20;       for xb, yb in train\_loader:

&#x20;           optimizer.zero\_grad()              

&#x20;           loss = criterion(model(xb), yb)    

&#x20;           loss.backward()                    

&#x20;           optimizer.step()                   

&#x20;           train\_loss += loss.item() \* len(xb)  

&#x20;       train\_loss /= len(train\_loader.dataset)  



&#x20;       model.eval()

&#x20;       val\_loss, correct = 0, 0

&#x20;       with torch.no\_grad():                  

&#x20;           for xb, yb in val\_loader:

&#x20;               pred = model(xb)

&#x20;               val\_loss += criterion(pred, yb).item() \* len(xb)

&#x20;               correct += ((pred > 0.5) == yb).sum().item()

&#x20;       val\_loss /= len(val\_loader.dataset)

&#x20;       val\_acc = correct / len(val\_loader.dataset)





&#x20;       history\['train\_loss'].append(train\_loss)

&#x20;       history\['val\_loss'].append(val\_loss)

&#x20;       history\['val\_acc'].append(val\_acc)



&#x20;       if epoch % 10 == 0:

&#x20;           print(f"epoch {epoch:3d} train={train\_loss:.4f} val={val\_loss:.4f} acc={val\_acc:.2%}")



&#x20;   return history




* deverá existir um venv na raiz do projeto
* deverá ter o pytorch deverá usar cuda. 
* eu sei que meu ambiente usa torch==2.13.0+cu130, mas deve ter um fallback para cuda em cpu, pois outras pessoas farão testes no notebook em diferentes ambientes. 
* deverá existir um bloco com constantes para alguns hiperparametros e valores necessários para o treino. 






