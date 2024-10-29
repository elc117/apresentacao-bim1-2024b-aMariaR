# Lista de apresentações BoudingBoxes
# Função 1:

Crie uma função para obter as bounding boxes de uma dada classe. Essa função deve receber um número representando a classe, a lista de bounding boxes e a lista de classes. Resolva esta função sem usar lambda, só usando outras funções existentes ou que você declarar. Pesquise a função zip, que será útil aqui.

Nome e tipo da função:
selectBoundingBoxesForClass :: Int -> [(Float, Float, Float, Float)] -> [Int] -> [(Float, Float, Float, Float)]

# A função:

```haskell
-- Bounding boxes: (xmin, ymin, xmax, ymax)
boundingBoxes :: [(Float, Float, Float, Float)]
boundingBoxes = [(34.0, 60.0, 200.0, 320.0),
                 (100.0, 150.0, 250.0, 380.0),
                 (300.0, 220.0, 450.0, 450.0)]

-- Scores: Confidence scores for each detection
scores :: [Float]
scores = [0.95, 0.80, 0.60]

-- Classes: Class 0 or 1 representing two object types
classes :: [Int]
classes = [0, 1, 0]

-- Convert class list from Int to Float
convertFloat :: [Int] -> [Float]
convertFloat list = map fromIntegral list

-- Check if the class of bounding box matches the specified class
verifyEqual :: Int -> (Float, (Float, Float, Float, Float)) -> Bool
verifyEqual classeR (classe, _) = classe == fromIntegral classeR

-- Select bounding boxes for a specified class
selectBoundingBoxesForClass :: Int -> [(Float, Float, Float, Float)] -> [Int] -> [(Float, Float, Float, Float)]
selectBoundingBoxesForClass classRecebida listaBB listaClass =
  map snd (filter (verifyEqual classRecebida) listaCBB)
  where listaCBB = zip (convertFloat listaClass) listaBB
```
# Resultados dos testes:

ghci> selectBoundingBoxesForClass 0 boundingBoxes classes
[(34.0,60.0,200.0,320.0),(300.0,220.0,450.0,450.0)]
ghci> selectBoundingBoxesForClass 1 boundingBoxes classes
[(100.0,150.0,250.0,380.0)]

# Função poderia ser resolvida com list comprehension:

```haskell
-- Bounding boxes: (xmin, ymin, xmax, ymax)
boundingBoxes :: [(Float, Float, Float, Float)]
boundingBoxes = [(34.0, 60.0, 200.0, 320.0),
                 (100.0, 150.0, 250.0, 380.0),
                 (300.0, 220.0, 450.0, 450.0)]

-- Scores: Confidence scores for each detection
scores :: [Float]
scores = [0.95, 0.80, 0.60]

-- Classes: Class 0 or 1 representing two object types
classes :: [Int]
classes = [0, 1, 0]

-- Convert class list from Int to Float
convertFloat :: [Int] -> [Float]
convertFloat list = [fromIntegral x | x <- list]

-- Select bounding boxes for a specified class using list comprehension
selectBoundingBoxesForClass :: Int -> [(Float, Float, Float, Float)] -> [Int] -> [(Float, Float, Float, Float)]
selectBoundingBoxesForClass classRecebida listaBB listaClass = 
  [bb | (classe, bb) <- zip (convertFloat listaClass) listaBB, classe == fromIntegral classRecebida]
```

# Pontos a serem destacados:

-Uso de _ ;

-Uso de fromItegral;

-Uso de zip;


# Fontes:
-Arquivos da professora disponíveis em: https://github.com/AndreaInfUFSM/elc117-2024b






