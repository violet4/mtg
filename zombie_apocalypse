#!/usr/bin/env python
import sys


def print_current_info(c, ssz, az, l, end='\n'):
    print(f'counter: {c}; sick: {ssz}; attacking: {az}; life: {l}', end=end)


def process_int(msg=None):
    print()
    if msg:
        print(msg, '[0] ', end='')
    val = input()
    if not val:
        return 0
    return int(val)


def main(mode):

    print(f'\n{mode} mode\n')

    counter = 1
    attacking_zombies = 0
    summon_sickness_zombies = 0
    life = 40


    print_current_info(counter, summon_sickness_zombies, attacking_zombies, life)

    while life > 0:
        print(f'\nyour turn #{counter}\n', end='')
        print('how much damage do you deal to the zombie overlord? how many zombies do you kill?\nfirst: ', end='')
        damage = process_int('how much damage do you deal to the zombie overlord?')
        life -= damage
        print(f'zombies at {life} life\n')

        if summon_sickness_zombies + attacking_zombies > 0:
            print(f'sick: {summon_sickness_zombies}; can attack: {attacking_zombies}; total: {summon_sickness_zombies+attacking_zombies}')
            zombies_die = process_int('how many zombies do you kill?')
            zombies_die = max(0, zombies_die)
            if zombies_die > attacking_zombies:
                zombies_die -= attacking_zombies
                attacking_zombies = 0
                summon_sickness_zombies -= zombies_die
                summon_sickness_zombies = max(0, summon_sickness_zombies)
            else:
                attacking_zombies -= zombies_die
                attacking_zombies = max(0, attacking_zombies)


        counter_text = 'counter   '
        ssz_text = 'summon sickness zombies'
        az_text = 'attacking zombies'
        l = [[counter_text, '|', ssz_text, '|', az_text]]
        l.append([str(counter), '=>', summon_sickness_zombies, '=>', attacking_zombies])
        attacking_zombies += summon_sickness_zombies
        # l.append([str(counter), '=>', summon_sickness_zombies, '|', attacking_zombies])

        if mode == 'easy':
            summon_sickness_zombies = counter - attacking_zombies
        else:
            summon_sickness_zombies = counter
        l.append([f'{counter}+1 => {counter+1}', '|', summon_sickness_zombies, '|', attacking_zombies])

        row = '{{: >{}}} {{: >2}} {{: >{}}} {{: >2}} {{: >{}}}'.format(str(len(counter_text)), str(len(ssz_text)), str(len(az_text)))
        for r in l:
            print(row.format(*r))
        # print_current_info(counter, summon_sickness_zombies, attacking_zombies, life)
        if attacking_zombies:
            print('\n\n### zombies attack!')
            print_current_info(counter, summon_sickness_zombies, attacking_zombies, life)
            print(f'{attacking_zombies} zombies attack. how much life does the zombie overlord lose from attacking you? how many are blocked and die? how many are blocked and live?')
            life_lost = process_int('first: how much life does the zombie overlord lose from attacking you?')
            if life_lost:
                life -= life_lost
                print(f'the zombies are at {life} life')

            die = process_int('how many are blocked and die?')
            attacking_zombies = max(0, attacking_zombies-die)
            causing_damage = attacking_zombies
            if attacking_zombies:
                blocked_and_live = process_int('how many are blocked and live?')
                causing_damage = attacking_zombies - blocked_and_live
            causing_damage = max(causing_damage, 0)
            print(f'\n### {causing_damage} zombies get through. take {causing_damage*2} damage\n')
        # input('press enter to pass turn')
        counter += 1
        print_current_info(counter, summon_sickness_zombies, attacking_zombies, life)

    print(f'')


if __name__ == '__main__':
    if len(sys.argv) == 1:
        mode = input('(1) easy mode or (2) hard mode?')
    else:
        mode = sys.argv[1]
    mode = mode[0]
    if mode in '1e':
        mode = 'easy'
    elif mode in '2h':
        mode = 'hard'
    else:
        print("mode not recognized. choose '1' or 'e' for easy, or '2' or 'h' for hard")
        exit(2)
    main(mode)

