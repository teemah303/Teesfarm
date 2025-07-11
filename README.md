# Teesfarm
A mobile-based farm management system for animal farming, tracking animal health, inventory and financial 
import React, { useEffect, useState } from 'react';
import { View, Button, FlatList } from 'react-native';
import { supabase } from '../supabase';
import AnimalCard from '../components/AnimalCard';

export default function DashboardScreen({ navigation }) {
  const [animals, setAnimals] = useState([]);

  const fetchAnimals = async () => {
    const { data } = await supabase.from('animals').select('*');
    setAnimals(data);
  };

  useEffect(() => {
    fetchAnimals();
  }, []);

  return (
    <View>
      <Button title="Add Animal" onPress={() => navigation.navigate('AnimalForm')} />
      <FlatList
        data={animals}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => <AnimalCard animal={item} />}
      />
    </View>
  );
}