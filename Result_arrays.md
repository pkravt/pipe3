# Стационарный расчет #
Массивы результатов стационарного расчета в дельфи описаны в TBranch классе (BranchUnit.pas):
```
Loss_friction      : TFloatArray;  // index = segment number
Loss_local         : TFloatArray;  // index = segment number
Loss_sum           : TFloatArray;  // index = segment number
Loss_nivelir       : TFloatArray;  // index = segment number
Loss_accel         : TFloatArray;  // index = segment number
Loss_dL            : TFloatArray;  // index = segment number
Pressure           : TFloatArray;  // index = segment start
X_mfq              : TFloatArray;  // index = segment start
X_vfq              : TFloatArray;  // index = segment start
dens_gas_end       : TFloatArray;  // index = segment start
dens_gas           : TFloatArray;  // index = segment number (average over segment)
dens_tp_end        : TFloatArray;  // index = segment start
dens_tp            : TFloatArray;  // index = segment number (average over segment)
gas_flowrate       : TFloatArray;  // index = segment start
mix_flowrate       : TFloatArray;  // index = segment start
Vel_section        : TFloatArray;  // index = segment start
```

Все эти массивы имеют размерность [[ObjectsNum+1]] (несмотря на то,
что часть из них относится к целому сегменту). Для тех массивов,
которые содержат параметры в сечении трубопровода, а не в целом сегменте,
индекс массива соответствует геометрическому началу сегмента.
Т.е. для главной ветви Vel\_section[[0](0.md)] всегда будет содержать скорость
на входе в главную ветвь. Для расходной боковой ветви
скорость на входе будет Vel\_section[[ObjectsNum](ObjectsNum.md)].



# Нестационарный расчет #
Массивы результатов нестационарного расчета в дельфи описаны в TBranch классе (BranchUnit.pas):
```
tLoss_friction     : TFloatArray2;
tLoss_local        : TFloatArray2;
tLoss_sum          : TFloatArray2;
tLoss_nivelir      : TFloatArray2;
tLoss_accel        : TFloatArray2;
tLoss_dL           : TFloatArray2;
tPressure          : TFloatArray2;
tX_mfq             : TFloatArray2;
tX_vfq             : TFloatArray2;
tdens_gas_end      : TFloatArray2;
tdens_gas          : TFloatArray2;
tdens_tp_end       : TFloatArray2;
tdens_tp           : TFloatArray2;
tgas_flowrate      : TFloatArray2;
tmix_flowrate      : TFloatArray2;
tVel_section       : TFloatArray2;
```

Это точно такие же массивы, как и стационарные, только у них добавлено
второе измерение - временной шаг. Таким образом, на каждом шаге
нестационарного расчета стационарные результаты копируются из стационарных массивов в элемент нестационарного массива, соответствующий
текущему временному шагу.

Кроме того, дополнительно введены массивы для нестационарных результатов
расчета для всей ветки в целом:

```
tflow_rate         : TFloatArray;
tvelocity          : TFloatArray;
tfuel_level        : TFloatArray;
tfuel_level_RCV    : TFloatArray;
```

В них пишется на каждом шаге: массовый расход через ветку, скорость топлива в ветке (в точке присоединения для боковых ветвей, или FFS скорость для главной), уровень топлива в бачке ветки, и опционально уровень приемного бачка (для главной ветви). Эти четыре одномерных массива имеют размерность кол-ва временных шагов.