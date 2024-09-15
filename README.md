# rpg
dosGuriNeMeu

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Controle de Personagem RPG',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CharacterControlScreen(),
    );
  }
}

class Character {
  String name;
  double life;
  double sanity;
  TextEditingController controller;

  Character({required this.name, this.life = 100.0, this.sanity = 100.0})
      : controller = TextEditingController(text: name);
}

class CharacterControlScreen extends StatefulWidget {
  @override
  _CharacterControlScreenState createState() => _CharacterControlScreenState();
}

class _CharacterControlScreenState extends State<CharacterControlScreen> {
  final List<Character> characters = [
    Character(name: 'Personagem 1'),
    Character(name: 'Personagem 2'),
    Character(name: 'Personagem 3'),
    Character(name: 'Personagem 4'),
    Character(name: 'Personagem 5'),
  ];

  void _updateCharacter(int index, double value, bool isDamage) {
    setState(() {
      if (isDamage) {
        characters[index].life = (characters[index].life - value).clamp(0.0, 100.0);
      } else {
        characters[index].life = (characters[index].life + value).clamp(0.0, 100.0);
      }
    });
  }

  void _updateSanity(int index, double value, bool isLoss) {
    setState(() {
      if (isLoss) {
        characters[index].sanity = (characters[index].sanity - value).clamp(0.0, 100.0);
      } else {
        characters[index].sanity = (characters[index].sanity + value).clamp(0.0, 100.0);
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Controle de Personagens RPG'),
      ),
      body: Stack(
        children: [
          // Imagem de fundo
          Image.network(
            'data:image/jpeg;base64,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', // Substitua pela URL da sua imagem de fundo
            width: double.infinity,
            height: double.infinity,
            fit: BoxFit.cover,
          ),
          ListView.builder(
            itemCount: characters.length,
            itemBuilder: (context, index) {
              final character = characters[index];
              return Card(
                margin: EdgeInsets.all(8),
                child: Padding(
                  padding: EdgeInsets.all(16),
                  child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      TextField(
                        controller: character.controller,
                        onChanged: (value) {
                          setState(() {
                            character.name = value;
                          });
                        },
                        decoration: InputDecoration(
                          labelText: 'Nome do Personagem',
                          border: OutlineInputBorder(),
                        ),
                        textAlign: TextAlign.start,
                      ),
                      SizedBox(height: 8),
                      Row(
                        children: [
                          // Imagem do coração
                          Image.network(
                            'data:image/jpeg;base64,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', // Substitua pela URL da imagem de coração
                            width: 24,
                            height: 24,
                          ),
                          SizedBox(width: 8),
                          Text('Vida: ${character.life.toStringAsFixed(1)}/100'),
                        ],
                      ),
                      Stack(
                        children: [
                          Container(
                            width: double.infinity,
                            height: 24,
                            decoration: BoxDecoration(
                              color: Colors.grey[300],
                              borderRadius: BorderRadius.circular(8),
                            ),
                          ),
                          Container(
                            width: (character.life / 100) * MediaQuery.of(context).size.width,
                            height: 24,
                            decoration: BoxDecoration(
                              color: Colors.red,
                              borderRadius: BorderRadius.circular(8),
                            ),
                          ),
                        ],
                      ),
                      SizedBox(height: 8),
                      Row(
                        children: [
                          // Imagem do cérebro
                          Image.network(
                            'data:image/jpeg;base64,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', // Substitua pela URL da imagem de cérebro
                            width: 24,
                            height: 24,
                          ),
                          SizedBox(width: 8),
                          Text('Sanidade: ${character.sanity.toStringAsFixed(1)}/100'),
                        ],
                      ),
                      Stack(
                        children: [
                          Container(
                            width: double.infinity,
                            height: 24,
                            decoration: BoxDecoration(
                              color: Colors.grey[300],
                              borderRadius: BorderRadius.circular(8),
                            ),
                          ),
                          Container(
                            width: (character.sanity / 100) * MediaQuery.of(context).size.width,
                            height: 24,
                            decoration: BoxDecoration(
                              color: Colors.blue,
                              borderRadius: BorderRadius.circular(8),
                            ),
                          ),
                        ],
                      ),
                      SizedBox(height: 8),
                      Row(
                        children: [
                          ElevatedButton(
                            onPressed: () => _updateCharacter(index, 10, true), // Causar 10 de dano
                            child: Text('Causar 10 de Dano'),
                          ),
                          SizedBox(width: 8),
                          ElevatedButton(
                            onPressed: () => _updateCharacter(index, 10, false), // Recuperar 10 de Vida
                            child: Text('Recuperar 10 de Vida'),
                          ),
                          SizedBox(width: 8),
                          ElevatedButton(
                            onPressed: () => _updateSanity(index, 10, true), // Perder 10 de Sanidade
                            child: Text('Perder 10 de Sanidade'),
                          ),
                          SizedBox(width: 8),
                          ElevatedButton(
                            onPressed: () => _updateSanity(index, 10, false), // Recuperar 10 de Sanidade
                            child: Text('Recuperar 10 de Sanidade'),
                          ),
                        ],
                      ),
                    ],
                  ),
                ),
              );
            },
          ),
        ],
      ),
    );
  }
}
